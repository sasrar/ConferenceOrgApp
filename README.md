# A Conference Organization Application

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
2. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
3. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
4. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
5. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
6. (Optional) Generate your client library(ies) with [the endpoints tool][6].
7. Deploy your application.
8. Go to API explorer site on local by typing "_ah/api/explorer" to end of local url (do the same on deployed site)
9. Execute the different api methods in the API explorer (do the same on deployed site)

[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool

## Conference
A Conference object holds information about a conference event. This includes:
* name			: this is required
* description
* organizerUserId	: this is used to identify the user that created this conference
* topics
* city
* startDate
* month
* endDate
* maxAttendees		: the maximum number of seats that can be occupied at this conference
* seatsAvailable	: the number of seats that are left for this conference

### Creating a conference
A conference can be created using the <b>createConference</b> API method. The user passes all the data pertaining to a conference
which is parsed and put into the datastore as a Conference entity.

### Getting created conferences
A user can get all the conferences they've created by using the <b>getConferencesCreated</b> endpoint method.

## Session
A Conference can have session(s). Each session object holds information about a conference session. This includes:
* name			: this is required
* highlights
* speaker
* duration
* typeOfSession
* date
* startTime

## Additional Queries
Two additional queries have been added to the application.

	1. getOldSessions(): returns sessions that take place before 12/01/05
	2. getNewSessions(): returns sessions that take place after 01/01/10

Another query has been implemented to return non-Workshop sessions that take place before before 7P. Google App Engine currently does not allow multiple inequality operators on different properties for a single query. To overcome this error I implemented two separate queries. 

The first returns sessions that are not of type 'Workshop'.
The second returns sessions that take place before 7P.
I then return the intersection of both queries.
