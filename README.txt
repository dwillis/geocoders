Geocoders
=========

Code for accessing various geocoding web services with an ultra simple API:

    name, (lon, lat) = geocode('london')

The geocode functions return (unicode_place_name, (float_lon, float_lat)) if
the string can be geocoded, and (None, (None, None)) if it cannot. The ordering
of the coordinates makes it possible to pass them directly to a Point object in
GeoDjango (using the GEOS API):

>>> from django.contrib.gis.geos import *
>>> from geocoders.google import geocoder
>>> geocode = geocoder('GOOGLE-API-KEY')
>>> results = geocode('new york')
(u'New York, NY, USA', (-73.986951000000005, 40.756053999999999))
>>> pnt = Point(results[1])

Currently supported: Google Geocoder, Yahoo! Geocoder, Yahoo! Placemaker,
GeoNames and Multimap.

Google:

>>> from geocoders.google import geocoder
>>> geocode = geocoder('GOOGLE-API-KEY')
>>> geocode('new york')
(u'New York, NY, USA', (-73.986951000000005, 40.756053999999999))
>>> geocode('oneuth')
(u'South, Bloomfield, NY 14469, USA', (-77.5385449999999, 42.865267000000003))

Yahoo!:

>>> from geocoders.yahoo import geocoder
>>> geocode = geocoder('YAHOO-API-KEY')
>>> geocode('new york')
(u'New York, NY, US', (-74.007124000000005, 40.714550000000003))
>>> geocode('oneuth')
(u'Aneth, UT 84510, US', (-109.189911, 37.217799999999997))

Yahoo! Placemaker:

>>> from geocoders.placemaker import geocoder
>>> geocode = geocoder('YAHOO-API-KEY')
>>> geocode('new york')
(u'New York, NY, US', (-74.007099999999994, 40.714500000000001))
>>> geocode('oneuth')
(None, (None, None))

While Yahoo! Placemaker isn't strictly designed as a geocoder, in practice it
can be useful for things like "did you mean location X" in a regular search
engine.

GeoNames:

>>> from geocoders.geonames import geocoder
>>> geocode('new york')
(u'New York', (-74.005972900000003, 40.714269100000003))
>>> geocode('oneuth')
(None, (None, None))

Multimap:

>>> from geocoders.multimap import geocoder
>>> geocode = geocoder('MULTIMAP-API-KEY')
>>> geocode('new york')
('New York, State of New York, United States', ('-75.49990', '43.00035'))
>>> geocode('oneuth')
('Omeath, Louth', ('-6.26070', '54.08790'))