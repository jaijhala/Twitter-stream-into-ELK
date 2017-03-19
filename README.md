# Twitter-stream-into-ELK
Example to feed twitter stream

In this example, we will feed the twitter streams related to Security content into ELK stack. Data flow would look like -> 
Twitter stream -> Logstash -> Elasticsearch -> Kibana

1). You will need to create a twitter app from here -> https://apps.twitter.com/
Once you create that, keep note of the API Keys and Access Tokens. 

2). Create a file twitter_logstash.conf and add following contents -> 

input {
  twitter {
    consumer_key       => "YOUR CONSUMER KEY"
    consumer_secret    => "YOUR SECRET KEY"
    oauth_token        => "YOUR TOKEN"
    oauth_token_secret => "YOUR TOKEN SECRET"
    keywords           =>["hack", "breach","cybersecurity", "malware","cybercrime","cyberattack"]
    full_tweet         => true
  }
}

filter { }

output {
  stdout {
    codec => dots
  }
  elasticsearch {
      hosts => "localhost:9200"
      index         => "twitter-feed"
      document_type => "tweets"
      template      => "elastic/twitter_elastic_example/twitter_template.json"
      template_name => "twitter_feed"
      template_overwrite => true
  }
}

You can modify the keywords above as per your need.

3). Run elasticsearch and Kibana. 
  Start feeding twitter data by running Logstash with the above conf file. 
  
4). Please refer to attached sample Dashboard. 
