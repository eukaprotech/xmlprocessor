# Description

An android asynchronous xml processor based on XmlPullParser, targeting RSS.

# Getting Started

Add the dependency in build.gradle (App module)

```compile 'com.eukaprotech.xmlprocessor:xmlprocessor:1.0.0@aar'```

# Usage Example

To process an xml string already loaded from a file or an RSS feed. The xml string will be processed into a JSONObject list, HashMap list or JSONArray.

A sample xml_string response from an RSS feed. 

                      <rss version="2.0">
                          <channel>
                          <title>Music Industry</title>
                          <link>https://www.einnews.com/news/newsfeed_music</link>
                          <description/>
                          <generator>EIN News</generator>
                          <item>
                              <title>
                              'The status quo will be obliterated!' – the inventors making their own musical instruments
                              </title>
                              <link>
                              https://www.einnews.com/article/417438078/V3TJlquqo0Ojg5t7?ref=rss&ecode=3wHjNW-Lw4Tcr_9P
                              </link>
                              <guid isPermaLink="false">https://www.einnews.com/article/417438078</guid>
                              <pubDate>Fri, 24 Nov 2017 08:04:13 GMT</pubDate>
                              <description>
                              &#8230; kept. If someone turned their <span class="match">music</span> up too loud, you imagine &#8230; have travelled there, too. The <span class="match">music</span> keeps changing location with &#8230; ‘It will change the way <span class="match">music</span> functions’ … Subhraag Singh with &#8230; won this year’s Guthman <span class="match">musical</span> instrument competition at Georgia &#8230;
                              </description>
                          </item>
                          <item>
                              <title>Do You Have News to Share? Get It Published.</title>
                              <link>
                              https://www.einnews.com/article/417465808/SVgKa5jGvEeh4_1Z?ref=rss&ecode=3wHjNW-Lw4Tcr_9P
                              </link>
                              <guid isPermaLink="false">
                              https://www.einnews.com/article/417465808/SVgKa5jGvEeh4_1Z
                              </guid>
                              <pubDate>Fri, 24 Nov 2017 12:09:36 GMT</pubDate>
                              <description>
                              With EIN Presswire press release distribution services you will reach decision makers and journalists plus get valuable SEO benefits.
                              </description>
                          </item>
                          </channel>
                       </rss>;

The required records have the tag "item". Each record has elements with the tags "title", "description", "link", "pubDate" and "guid".

Take "item" as the entryTag. Take "title", "description", "link", "pubDate" and "guid" as entryKeys.

Method 1.

                String entryTag = "item";
                ArrayList<String> entryKeys = new ArrayList<>();
                entryKeys.add("title");
                entryKeys.add("description");
                entryKeys.add("link");
                entryKeys.add("pubDate");
                RssXmlProcessor xmlProcessor = new RssXmlProcessor(entryTag, entryKeys);
                xmlProcessor.execute(xml_string, new RssXmlToHashMapListHandler() {
                    @Override
                    public void onStart() {
                        
                    }

                    @Override
                    public void onSuccess(List<HashMap<String, String>> items) {
                          //consuming the processed items using the same keys
                          for(HashMap<String, String> item: items) {
                                String title = item.get("title");
                                String description = item.get("description");
                                String link = item.get("link");
                                String pubDate = item.get("pubDate");
                          }
                    }

                    @Override
                    public void onFail(Exception ex) {
                        
                    }

                    @Override
                    public void onComplete() {
                        
                    }
                });
                
Method 2.

                String entryTag = "item";
                ArrayList<String> entryKeys = new ArrayList<>();
                entryKeys.add("title");
                entryKeys.add("description");
                entryKeys.add("link");
                entryKeys.add("pubDate");
                RssXmlProcessor xmlProcessor = new RssXmlProcessor(entryTag, entryKeys);
                xmlProcessor.execute(xml_string, new RssXmlToJSONListHandler() {
                    @Override
                    public void onStart() {
                        
                    }

                    @Override
                    public void onSuccess(List<JSONObject> items) {
                          //consuming the processed items using the same keys
                          for(JSONObject item: items) {
                              try {
                                  String title = item.getString("title");
                                  String description = item.getString("description");
                                  String link = item.getString("link");
                                  String pubDate = item.getString("pubDate");
                              }catch (Exception ex){}
                           }
                    }

                    @Override
                    public void onFail(Exception ex) {
                        
                    }

                    @Override
                    public void onComplete() {
                        
                    }
                });
                
 Method 3.

                String entryTag = "item";
                ArrayList<String> entryKeys = new ArrayList<>();
                entryKeys.add("title");
                entryKeys.add("description");
                entryKeys.add("link");
                entryKeys.add("pubDate");
                RssXmlProcessor xmlProcessor = new RssXmlProcessor(entryTag, entryKeys);
                xmlProcessor.execute(xml_string, new RssXmlToJSONArrayHandler() {
                    @Override
                    public void onStart() {

                    }

                    @Override
                    public void onSuccess(JSONArray items) {
                          //consuming the processed items using the same keys
                          for(int i=0; i<items.length(); i++) {
                              try {
                                  JSONObject item = items.getJSONObject(i);
                                  String title = item.getString("title");
                                  String description = item.getString("description");
                                  String link = item.getString("link");
                                  String pubDate = item.getString("pubDate");
                              }catch (Exception ex){}
                           }
                    }

                    @Override
                    public void onFail(Exception ex) {
                        
                    }

                    @Override
                    public void onComplete() {

                    }
                });
