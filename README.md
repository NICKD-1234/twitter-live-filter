# twitter-live-filter

A uni-based group cloud computing project aimed at introducing load balancing/auto-scaling concepts with Amazon Web Services. I.e., the user can provide a range of search terms   which will then be used to find tweets related to these terms. The Twitter API is used to ascertain a stream of tweets, which are then analysed using a natural language processing (NLP) library such as NLTK. The application scales in accordance with the CPU utilisation of a single instance. My primary reponsibility for this project, was the 'twitter-live-filter-api' which connect the front-end client application and the application used to consume the Twitter API. 

## Architecture
AWS ElastiCache with Redis for caching, and S3 buckets for longer term storage were utilised. 

![image](https://user-images.githubusercontent.com/62277610/143381293-0d1a65b8-e74b-4cc7-a1f7-e7c8a0cecc6b.png)

## Twitter-Stream-Api
The Twitter-Stream-Api is responsible for directly communicating with and consuming the Twitter API. Its purpose is to act as a middleman between the Twitter API and all of the instances of the scalable application. The main purpose of this API is to act as a workaround to the single connection limit of the Twitter API. This application simply runs on its own single instance and provides the Twitter Stream to connected clients. 

## Twitter-Live-Filter-Api
The Twitter-Live-Filter-Api is the scalable application which consumes the Twitter-Stream-Api application. Its primary responsibility is to filter through tweets using the query parameters provided by the client. The Natural’s Libraries tokenization and sentiment analysis is utilised for this process. It’s also responsible for storing tweets in Cache and storage, and fetching those tweets if a similar request is made. These tweets are then displayed to the user while they wait for further live tweets.  

## Twitter-Live-Filter-Client
This is the client application used to graphically display the tweets to the user on a simple ui (as the primary purpose of the project was to demonstrate load balancing). It allows a user to enter keywords which are sent to the Twitter-Live-Filter-Api application. 

![image](https://user-images.githubusercontent.com/62277610/143381564-eb8e733c-0f7c-47f2-8bd8-e74cb7025467.png)

