# api-google-map
a python code that can use a public API key to request the current travel distance and duration between two gps position



#  pip install requests
#  pip install haversine
 
import haversine as hs
import googlemaps 
import requests
import webbrowser
from datetime import datetime
 
address = "bocom akwa-nord"
api_key = "AIzaSyA4GskVuacaoKJTKN6LFjgRwLk0XZ0hd28"
api_response = requests.get('https://maps.googleapis.com/maps/api/geocode/json?address={0}&key={1}'.format(address, api_key))
api_response_dict = api_response.json()
 
 # Requires API key 
gmaps = googlemaps.Client(api_key)  
 # Requires cities name 
distanceUsingNames = gmaps.distance_matrix('bocom akwa-nord','deido')['rows'][0]['elements'][0]
 
 # Requires geo-coordinates(latitude/longitude) of origin and destination
origin_latitude = 9.710126
origin_longitude = 4.088327
destination_latitude = 9.713932
destination_longitude = 4.065305
distanceCoordinates = gmaps.distance_matrix([str(origin_latitude) + " " + str(origin_longitude)], [str(destination_latitude) + " " + str(destination_longitude)], mode='driving')['rows'][0]['elements'][0]
now = datetime.now()
directions_result = gmaps.directions("Sydney Town Hall","Parramatta, NSW",mode="transit",departure_time=now)
 
print(distanceCoordinates['duration'])
 
 
 # if api_response_dict['status'] == 'OK':
 #     latitude = api_response_dict['results'][0]['geometry']['location']['lat']
 #     longitude = api_response_dict['results'][0]['geometry']['location']['lng']
 #     print 'Latitude:', latitude
 #     print 'Longitude:', longitude
 
 
 
 # loc1 and loc2 are various values gottten from the geo-location api 
 
loc1=(28.426846,77.088834)
loc2=(28.394231,77.050308)
print(hs.haversine(loc1,loc2))
br = "https://www.google.com/maps/embed/v1/directions?key=AIzaSyA4GskVuacaoKJTKN6LFjgRwLk0XZ0hd28&origin=Oslo+Norway&destination=Telemark+Norway&avoid=tolls%7Chighways"
 
f = open('test.html', 'w')
message = """<html>
 <head></head>
 <body><iframe src="https://www.google.com/maps/embed/v1/directions?key=AIzaSyA4GskVuacaoKJTKN6LFjgRwLk0XZ0hd28&origin=bocom akwa-nord&destination=deido&avoid=tolls%7Chighways" height="1024" width="1024" title="Iframe Example"></iframe></body>
 </html>"""


f.write(message)
webbrowser.open('test.html')
