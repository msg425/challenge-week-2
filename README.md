# Name

Manpreet Singh

# How many points have you earned?

100/100

(Make your own calculation and replace the number 0 with the points you think you've earned.)

# Show and tell (10 points)

[title-of-the-article] http://makezine.com/projects/smart-remote-control/

# Checkpoints

## Checkpoint 1 (5 points)

![Imgur](http://i.imgur.com/zXvwRM4.png)

## Checkpoint 2 (5 points)

![Imgur](http://i.imgur.com/KbEOhg2)

## Checkpoint 3 (5 points)

![Imgur](http://i.imgur.com/El0FY55)

## Checkpoint 4 (5 points)

![Imgur](http://i.imgur.com/6q4J3D9)

## Study Questions (3 points x 4 = 12 points)

### Q1. (3 points)

The three names probably represent three different servers. There are three of these because having multiple servers helps in case of heavy traffic.

### Q2. (3 points)

Including “status=200” in queries helps ensure that only thse results are retrned which represent successfully completed transactions.

### Q3. (3 points)

Using the pipe operator in queries helps in cases where the search parameters are either unknown or variable, and need information from the results of another query etc. The alternative would be to run a search, use the results of that search for another query and so  on. This would take a lot of time and would be prone to error.

### Q4. (3 points)

Saving all the product purchase behavior in sructural databases would lead to a huge and slow-to-traverse database, which is highly undesirable. Also

# Challenges

## Challenge 1-a (2 points)
```
sourcetype=access_* | stats count 
```
![Imgur](http://i.imgur.com/jqHknYi.png)

## Challenge 1-b (2 points)
```
sourcetype=access_* | stats count AS "Events"
```
![Imgur](http://i.imgur.com/34tb0ly)

## Challenge 1-c (2 points)
```
sourcetype=access_* | stats count AS "Events", count(eval(action="purchase")) AS "Purchases"
```
![Imgur](http://i.imgur.com/vNzTbtL)

## Challenge 1-d (2 points)
```
sourcetype=access_* | stats count AS "Events", count(eval(action="purchase")) as "Purchases", count(eval(action="addtocart")) as "AddToCarts", count(eval(action="remove")) as "Removes"
```
![Imgur](http://i.imgur.com/4EST5Rd)

## Challenge 1-e (2 points)
```
sourcetype=access_* | stats max(bytes)
```
![Imgur](http://i.imgur.com/EvyCDcJ)

## Challenge 1-f (2 points)
```
sourcetype=access_* | stats max(bytes)
```
![Imgur](http://i.imgur.com/iO9jIVc)

## Challenge 1-g (2 points)
```
sourcetype=access_* | stats max(bytes) AS "MAX"
```
![Imgur](http://i.imgur.com/UUdzUc9)

## Challenge 1-h (2 points)
```
sourcetype=access_* | stats max(bytes) AS "MAX", min(bytes) AS "MIN", avg(bytes) AS "AVG"
```
![Imgur](http://i.imgur.com/JYucKJk)

## Challenge 1-i (2 points)
```
sourcetype=access_* | stats dc(productId) as "NumberofUniqueProducts", values(productId) as "UniqueProductIds"
```
![Imgur](http://i.imgur.com/wK6SWeB)


## Challenge 2-a (2 points)
```
sourcetype=access_* productId cart.do | top clientip
```
![Imgur](http://i.imgur.com/go8ps69.png)

## Challenge 2-b (2 points)
```
sourcetype=access_* productId cart.do | top date_wday limit=3
```
![Imgur](http://i.imgur.com/XPuW2Mo)

## Challenge 2-c (2 points)
```
sourcetype=access_* productId cart.do | top productId
```
![Imgur](http://i.imgur.com/dZ5sifM)


## Challenge 2-d (2 points)
```
sourcetype=access_* productId cart.do date_wday="friday" | top productId
```
![Imgur](http://i.imgur.com/6MBMyjq)

## Challenge 2-e (2 points)
```
sourcetype=access_* productId cart.do date_wday="friday" action="purchase" | top productId
```
![Imgur](http://i.imgur.com/tgf3uPE)

## Challenge 2-f (2 points)
```
sourcetype=access_* productId cart.do action="purchase" | top productId limit=1
```
![Imgur](http://i.imgur.com/Mp2cLmF)

## Challenge 2-g (2 points)
```
sourcetype=access_* productId cart.do action="purchase" | top productId by date_wday limit=1
```
![Imgur](http://i.imgur.com/yLvPfGz)

## Challenge 3-a (2 points)
```
sourcetype=access_* productId=* | timechart count
```
![Imgur](http://i.imgur.com/nrYtBQM.png)

## Challenge 3-b (2 points)
```
sourcetype=access_* productId=* | timechart dc(clientip)
```
![Imgur](http://i.imgur.com/FUal1H2)

## Challenge 3-c (2 points)
```
sourcetype=access_* productId=* | timechart dc(clientip) AS "UniqueIPs" span=1h
```
![Imgur](http://i.imgur.com/fq2mlKC)

## Challenge 3-d (2 points)
```
sourcetype=access_* productId=* | timechart count by source
```
![Imgur](http://i.imgur.com/2Do3r6F)

## Challenge 3-e (2 points)
```
sourcetype=access_* productId=* | timechart count by productId
```
![Imgur](http://i.imgur.com/GHIgJn0)

## Challenge 3-f (2 points)
```
sourcetype=access_* productId=* | timechart count by productId limit=16
```
![Imgur](http://i.imgur.com/hMrSuEk)

## Challenge 3-g (2 points)
```
sourcetype=access_* productId=* | timechart count by clientip
```
![Imgur](http://i.imgur.com/2DATcbU)

## Challenge 3-h (2 points)
```
sourcetype=access_* productId=* | timechart count by clientip useother=f
```
![Imgur](http://i.imgur.com/SqEYo2f)

## Challenge 3-i (2 points)
```
sourcetype=access_* productId=* | timechart sum(bytes) span=1h
```
![Imgur](http://i.imgur.com/snRRUqf)

## Challenge 4-a (4 points)
```
sourcetype=access_* | rex "(?<mymethod>GET)" | table mymethod, method, _raw
```
![Imgur](http://i.imgur.com/pX5dM5Y.png)

## Challenge 4-b (4 points)
```
sourcetype=access_* action | rex "(GET|POST) /cart.do\?action=(?<myaction>purchase)" | table myaction, action, _raw
