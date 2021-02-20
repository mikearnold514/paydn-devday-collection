# paydn-developer-day-collection
#
# This postman collection is intended for use during the PayDN Developer Day event.
# There is an API Key established in each API that will be valid only for the duration of the Developer Day event.
#
# To use this API you will need an API Key that will be provided at the Developer Day event.
# The API Key will be used in the Postman Collection where you see key=
#
# You will find the following APIs in this collection:
#
#    1.  Auth - these are the APIs that create and retrieve Payment Transactions
#    2.  Basket - these are the APIs that create and retrieve Baskets.  Baskets are analogous to a Shopping Cart and map to the Items section of the Auth APIs
#    3.  Consumer - these are the APIs that create and retrieve Consumers.  Consumer information is included in the Auth APIs.
#    4.  Merchant - these are the APIs that create and retrieve Merchants.  Merchant information is included in the Auth APIs.
#    5.  Program - these are the APIs that create and retrieve Programs.  Programs are Loyalty, Discount and Reward plans that Merchants can offer Consumers.  
#                  Program information is include in the Auth APIs.
#    6.  Products - these are the APIs that create and retrieve Products.  Products are used to build Baskets.  
#
# The PayDN API set described here is a demonstration only.  Edits are limted and are focused on primative data type validations and Postgres referencial integrity.
#
#
#
# This API set is intended to simulate a multi-lane retail merchant purchase scenario.  That is why you will see entities like Merchant, Consumer, Basket and so on.
# The unique approach to these payment transactions that PayDN is advancing is called the Multi-Party Synchronous Authorization (MPSA).
#
# Performing an MPSA transaction can be described as follows:
#
#    1.  A Consumer or a Merchant, using a mobile app, will generate a QR code.
#    2.  The QR Code will contain simple information for the purpose of this demo:
#        a.  Transaction Amount - This must be calculated by the cost of the Products in the Basket.
#        b.  Transaction Date/Time - This is just a timestamp.  It will be reset by the PayDN backend when the Authorization is completed.
#        c.  Correlation ID - This is a system generated ID that is obtained by the entity generating the QR Code by calling the /auths/getToken API.
#    3.  The entity who did not generate the QR Code will scan it.  Now the Correlation ID becomes a simple shared secret.
#    4.  Both the Merchant and Consumer will then submit their respective Authorization Requests.  Things to note:
#        a.  The submissions do not have to be at the exact same time.  They will be matched on the PayDN backend.
#        b.  Both submissions must be delivered within 1 minute of each other, for purposes of the demo, or the Token TTL will expire and you will have to start again.
#    5.  The Authorization Request will return one of two success messages:
#        a.  The first submission to be received will get a response of SUCCESS - Auth Pending Match
#        b.  The second submission to be received will get a response of SUCCESS - Auth Matched
#        c.  There will also be specific data elements in the response to help you retreive the Authorization payload and see the Response details in that payload.
#
#
# Here is the list of core APIs to perform a transaction given the test data already established in the Postgres Database.  
# Feel free to use the Consumer, Merchant, Baskets, Products and Programs APIs to populated the DB with records that 
# have more relevance for your industry so the demo experience is a relevant as possible.
#
#
#   1.  {{url}}/auths/getToken - this will return a unique token that you can use as the Correlation ID in the Auth APIs.
#                                The Correlation ID is what links the Consumer and Merchant Auth Requests.  It is a shared secret needed for the process to work.
#   2.  {{url}}/auths/consumer - use this API and the data in the QR Code and Consumer to generate a ConsumerAuthRequest.
#   3.  {{url}}/auths/merchant - ust this API and the data in the QR Code and Merchant plus the Basket and Program to generate a MerchantAuthRequest.
#
# Posting the Consumer and Merchant Auth Requests within 1 minute of one another and you will get a successful Authorization response.
#
#



 
