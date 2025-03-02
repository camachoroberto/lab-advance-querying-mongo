![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)
 
# Answers
 
### 1. All the companies that it's name match 'Babelgum'. Retrieve only their `name` field.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'name' : { \$eq: 'Babelgum'}},{'name':1, '_id':0});
#Compass Operations
<!-- Your Code Goes Here -->
FILTER: {'name' : 'Babelgum' }
PROJECT: {'name': 1, '_id': 0}
SORT:
COLLATION:
SKIP:
LIMIT:
 
### 2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by **number of employees**.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'number_of_employees': {$gt: 5000}},{'name': 1, '_id': 0, 'number_of_employees':1}).sort({'number_of_employees':1}).limit(20)
<!-- Your Code Goes Here -->
#Compass Operations
FILTER: {'number_of_employees' : {$gt : 5000}}
PROJECT: {'name':1, 'number_of_employees': 1, '_id': 0}
SORT: {"number_of_employees": 1}
COLLATION:
SKIP:
LIMIT: 20
 
### 3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fileds.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'founded_year':{$gte : 2000, $lte : 5000}},{'_id': 0, 'name' : 1, 'founded_year': 1})
<!-- Your Code Goes Here -->
#Compass Operations
FILTER: {'founded_year': {$gte : 2000,$lte : 5000}}
PROJECT:{'_id': 0, 'name' : 1, 'founded_year': 1}
SORT:
COLLATION:
SKIP:
LIMIT:
 
### 4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and:[{'founded_year': {$lt: 2100}}, {'ipo.valuation_amount': {$gte: 100000000}}]},{'_id': 0, 'name': 1, 'ipo.valuation_amount': 1})
 
### 5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and: [{'number_of_employees':{$lt: 1000}},{'founded_year':{$lt: 2005}}]},{'_id': 0,'name': 1,'founded_year':1, 'number_of_employees': 1}).sort({'number_of_employees': -1}).limit(10)
 
### 6. All the companies that don't include the `partners` field.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'partners': {$exists: false}})
 
### 7. All the companies that have a null type of value on the `category_code` field.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'category_code': null})
 
### 8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and: [{'number_of_employees': {$gt: 100}},{'number_of_employees':{$lt: 1000}}]},{'_id':0, 'name': 1, 'number_of_employees': 1})
 
### 9. Order all the companies by their IPO price descendently.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'ipo.valuation_amount': {$exists:true}}).sort({"ipo.valuation_amount": -1})
 
### 10. Retrieve the 10 companies with more employees, order by the `number of employees`
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({}).sort({'number_of_employees': -1}).limit(10)
 
### 11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'founded_month': {$gte: 7}}).limit(1000)
 
### 12. All the companies that have been 'deadpooled' after the third year.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.aggregate({$project: {_id : 0, name : 1, difference: {$subtract:["$deadpooled_year", "$founded_year"]}}},{ $match: { difference: { $gt: 3}}})
 
### 13. All the companies founded before 2000 that have and acquisition amount of more than 10.000.000
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and:[{'founded_year': {$lt: 2000}},{'acquisition.price_amount': {$gt: 10000000}}]})
 
### 14. All the companies that have been acquired after 2015, order by the acquisition amount, and retrieve only their `name` and `acquisiton` field.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'acquisition.acquired_year': {$gt: 2015}}, {'_id': 0, 'name': 1, 'acquisiton': 1 })
 
### 15. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({'founded_year': {$exists: true ,$ne: null}},{'_id': 0, 'name': 1, 'founded_year': 1}).sort({'founded_year': 1}))
 
### 16. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `aquisition price` descendently. Limit the search to 10 documents.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and: [{'founded_day':{$lte: 7}},{'acquisition.price_amount': {$exists: true, $ne: null}}]},{'_id': 0, 'name':1, 'acquisition.price_amount': -1}).sort({'acquisition.price_amount' : 1}).limit(10)
 
### 17. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascendant order.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and: [{'category_code': 'web'},{'number_of_employees': {$gt: 4000}}]}, {'_id': 0, 'name': 1, 'category_code': 1, 'number_of_employees': 1}).sort({'number_of_employees': -1})

### 18. All the companies which their acquisition amount is more than 10.000.000, and currency are 'EUR'.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and: [{'acquisition.price_amount': {$gt:10000000}},{'acquisition.price_currency_code': {$eq:'EUR'}}]},{'_id':0, 'name': 1, 'acquisition.price_amount':1,'acquisition.price_currency_code':1}).sort({'acquisition.price_amount':1 })
 
 
### 19. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.
<!-- Your Code Goes Here -->
#Shell operations
 > db.companies.find({'acquisition.acquired_month': {$exists: true, $ne: null, $lte: 4}},{'_id':0, 'name':1, 'acquisition':1}).limit(10).pretty()
 
### 20. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.
<!-- Your Code Goes Here -->
#Shell operations
> db.companies.find({$and:[{'founded_year':{$gte: 2000}},{'founded_year':{$lte: 2010}},{'acquisition.acquired_year': {$ne: 2011}}]})
 

