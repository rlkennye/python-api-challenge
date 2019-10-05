# python-api-challenge
Weather report for 500 cities around the world

# Dependencies and Setup
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import requests
import time
import json

# Import API key
import api_keys

# Incorporated citipy to determine city based on latitude and longitude
from citipy import citipy

# Output File (CSV)
output_data_file = "Weather_Info_Output.csv"

# Range of latitudes and longitudes
lat_range = (-90, 90)
lng_range = (-180, 180)

Generate Cities List

# List for holding lat_lngs and cities
lat_lngs = []
cities = []

# Create a set of random lat and lng combinations
lats = np.random.uniform(low=-90.000, high=90.000, size=1500)

lngs = np.random.uniform(low=-180.000, high=180.000, size=1500)
lat_lngs = zip(lats, lngs)

# Identify nearest city for each lat, lng combination
for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name
    
    # If the city is unique, then add it to a our cities list
    if city not in cities:
        cities.append(city)
    
# Print the city count to confirm sufficient count
len(cities)
576
Perform API Calls
# OpenWeatherMap API Key
api_key = api_keys.api_key

# Starting URL for Weather Map API Call
url = "http://api.openweathermap.org/data/2.5/weather?units=metric&APPID=" + api_key 

# Create empty lists to append the API data into lists 
CityName = []
Cloudiness = []
Country = []
Date_Info = []
Humidity = []
lat = []
lon = []
MaxT = []
MaxW = []
x = 1
y = 1

# Record each API Call 
print(f"Beginning Data Retrieval")
print(f"------------------------")

#Start generating Weather Info data 
for city in cities:  
    
    # We try for the possibility that a city does not exist and we account for it.  
    try: 
        response = requests.get(f"{url}&q={city}").json() 
        CityName.append(response["name"])
        Cloudiness.append(response["clouds"]["all"])
        Country.append(response["sys"]["country"])
        Date_Info.append(response["dt"])
        Humidity.append(response["main"]["humidity"])
        lat.append(response["coord"]["lat"])
        lon.append(response["coord"]["lon"])
        MaxT.append(response["main"]["temp_max"])
        MaxW.append(response["wind"]["speed"])
        city_name = response["name"]
        print(f"Processing Record {x} Set of {y}| {city_name}")
        
        # Increase Record count 
        x += 1
        if x > 50: # start new Record
            x = 1
            y += 1 # increase set count
        if x == 1 and y == 11: # We have 500 Cities, let's exit
            break
        # Adjusting speed of API Calls
        time.sleep(1.5)
        
    # skip if no city found
    except:
        print(f"City of {city_name} not found. Skipping...")
    continue
print(f"-----------------------") 
print(f"Data Retrieval Complete")
print(f"-----------------------")    

Beginning Data Retrieval
------------------------
Processing Record 1 Set of 1| Aksarayskiy
Processing Record 2 Set of 1| New Norfolk
Processing Record 3 Set of 1| Marzuq
Processing Record 4 Set of 1| Rikitea
Processing Record 5 Set of 1| East London
Processing Record 6 Set of 1| Hilo
Processing Record 7 Set of 1| Bandundu
Processing Record 8 Set of 1| Goryachegorsk
Processing Record 9 Set of 1| Vaini
Processing Record 10 Set of 1| Moerai
Processing Record 11 Set of 1| Alofi
Processing Record 12 Set of 1| Umtata
Processing Record 13 Set of 1| Willmar
Processing Record 14 Set of 1| Bakchar
Processing Record 15 Set of 1| Mar del Plata
Processing Record 16 Set of 1| Albany
Processing Record 17 Set of 1| Springdale
Processing Record 18 Set of 1| Bonavista
Processing Record 19 Set of 1| Arraial do Cabo
Processing Record 20 Set of 1| Paracuru
Processing Record 21 Set of 1| Iqaluit
Processing Record 22 Set of 1| Dikson
City of Dikson not found. Skipping...
Processing Record 23 Set of 1| Iskateley
Processing Record 24 Set of 1| Pevek
Processing Record 25 Set of 1| Kapaa
Processing Record 26 Set of 1| Cherskiy
Processing Record 27 Set of 1| Bambous Virieux
Processing Record 28 Set of 1| Am Timan
Processing Record 29 Set of 1| Gamba
Processing Record 30 Set of 1| Iberia
Processing Record 31 Set of 1| Sisimiut
Processing Record 32 Set of 1| Belaya Gora
Processing Record 33 Set of 1| Luanda
Processing Record 34 Set of 1| Mezen
Processing Record 35 Set of 1| Road Town
Processing Record 36 Set of 1| Ushuaia
Processing Record 37 Set of 1| Cape Town
City of Cape Town not found. Skipping...
City of Cape Town not found. Skipping...
Processing Record 38 Set of 1| Miri
Processing Record 39 Set of 1| Yellowknife
Processing Record 40 Set of 1| Marawi
Processing Record 41 Set of 1| Ilulissat
Processing Record 42 Set of 1| Aguimes
Processing Record 43 Set of 1| Busselton
Processing Record 44 Set of 1| Port Alfred
Processing Record 45 Set of 1| Itarema
Processing Record 46 Set of 1| Aurich
Processing Record 47 Set of 1| Comodoro Rivadavia
Processing Record 48 Set of 1| Borogontsy
Processing Record 49 Set of 1| Yar-Sale
Processing Record 50 Set of 1| Vestmannaeyjar
Processing Record 1 Set of 2| Zhigansk
Processing Record 2 Set of 2| Castro
Processing Record 3 Set of 2| Punta Arenas
Processing Record 4 Set of 2| Newcastleton
City of Newcastleton not found. Skipping...
Processing Record 5 Set of 2| Airai
Processing Record 6 Set of 2| Port-Gentil
Processing Record 7 Set of 2| Deputatskiy
Processing Record 8 Set of 2| Hermanus
Processing Record 9 Set of 2| Datong
Processing Record 10 Set of 2| Loandjili
Processing Record 11 Set of 2| Thompson
Processing Record 12 Set of 2| Qixingtai
Processing Record 13 Set of 2| Umm Lajj
Processing Record 14 Set of 2| Vilhena
Processing Record 15 Set of 2| Jamestown
Processing Record 16 Set of 2| Atuona
Processing Record 17 Set of 2| Barrow
Processing Record 18 Set of 2| Carnarvon
Processing Record 19 Set of 2| Xunchang
Processing Record 20 Set of 2| Petropavlovsk-Kamchatskiy
Processing Record 21 Set of 2| Puerto Ayora
Processing Record 22 Set of 2| Saskylakh
City of Saskylakh not found. Skipping...
Processing Record 23 Set of 2| Jaisalmer
Processing Record 24 Set of 2| Mikhaylovka
Processing Record 25 Set of 2| Port Hardy
Processing Record 26 Set of 2| Rajshahi
Processing Record 27 Set of 2| Saint-Philippe
Processing Record 28 Set of 2| Podyuga
Processing Record 29 Set of 2| Moyale
Processing Record 30 Set of 2| Port Moresby
Processing Record 31 Set of 2| Denta
Processing Record 32 Set of 2| Khatanga
Processing Record 33 Set of 2| Suhbaatar
Processing Record 34 Set of 2| Narsaq
Processing Record 35 Set of 2| Wahiawa
Processing Record 36 Set of 2| Kodiak
Processing Record 37 Set of 2| Avarua
City of Avarua not found. Skipping...
Processing Record 38 Set of 2| Show Low
Processing Record 39 Set of 2| Bredasdorp
City of Bredasdorp not found. Skipping...
Processing Record 40 Set of 2| Fortuna
Processing Record 41 Set of 2| Lannion
Processing Record 42 Set of 2| Mount Gambier
Processing Record 43 Set of 2| Port Shepstone
Processing Record 44 Set of 2| Penzance
Processing Record 45 Set of 2| Codrington
Processing Record 46 Set of 2| Namibe
Processing Record 47 Set of 2| Qaanaaq
Processing Record 48 Set of 2| Namatanai
Processing Record 49 Set of 2| Ponta do Sol
Processing Record 50 Set of 2| Srednekolymsk
Processing Record 1 Set of 3| San Severino Marche
Processing Record 2 Set of 3| Cayenne
Processing Record 3 Set of 3| Georgetown
Processing Record 4 Set of 3| Kuliyapitiya
Processing Record 5 Set of 3| Ilheus
Processing Record 6 Set of 3| Lebanon
Processing Record 7 Set of 3| Tasiilaq
Processing Record 8 Set of 3| Kuybysheve
Processing Record 9 Set of 3| Northam
Processing Record 10 Set of 3| Nome
Processing Record 11 Set of 3| Tecoanapa
Processing Record 12 Set of 3| Sistranda
Processing Record 13 Set of 3| Chokurdakh
Processing Record 14 Set of 3| Puri
Processing Record 15 Set of 3| Buala
Processing Record 16 Set of 3| Moron
Processing Record 17 Set of 3| Hutchinson
Processing Record 18 Set of 3| Seoul
City of Seoul not found. Skipping...
City of Seoul not found. Skipping...
Processing Record 19 Set of 3| Mataura
Processing Record 20 Set of 3| Longyearbyen
Processing Record 21 Set of 3| Tshela
Processing Record 22 Set of 3| Butaritari
Processing Record 23 Set of 3| Ati
Processing Record 24 Set of 3| Progreso
Processing Record 25 Set of 3| Solnechnyy
City of Solnechnyy not found. Skipping...
Processing Record 26 Set of 3| Ust-Kulom
Processing Record 27 Set of 3| Lebu
City of Lebu not found. Skipping...
Processing Record 28 Set of 3| Lagoa
Processing Record 29 Set of 3| Aktau
Processing Record 30 Set of 3| Batman
Processing Record 31 Set of 3| Ionia
Processing Record 32 Set of 3| Lompoc
Processing Record 33 Set of 3| Carballo
City of Carballo not found. Skipping...
Processing Record 34 Set of 3| Havoysund
Processing Record 35 Set of 3| Ihosy
Processing Record 36 Set of 3| Portland
Processing Record 37 Set of 3| Vangaindrano
Processing Record 38 Set of 3| Nikolskoye
Processing Record 39 Set of 3| Esperance
Processing Record 40 Set of 3| Faanui
Processing Record 41 Set of 3| Aykhal
City of Aykhal not found. Skipping...
Processing Record 42 Set of 3| Nadym
Processing Record 43 Set of 3| Los Llanos de Aridane
Processing Record 44 Set of 3| Port Lincoln
City of Port Lincoln not found. Skipping...
Processing Record 45 Set of 3| Tall Kayf
Processing Record 46 Set of 3| Lixourion
City of Lixourion not found. Skipping...
Processing Record 47 Set of 3| Havelock
Processing Record 48 Set of 3| Bulaevo
Processing Record 49 Set of 3| Damghan
Processing Record 50 Set of 3| Kilindoni
Processing Record 1 Set of 4| Bluff
Processing Record 2 Set of 4| Yulara
Processing Record 3 Set of 4| Nemuro
Processing Record 4 Set of 4| Cidreira
Processing Record 5 Set of 4| Nantucket
Processing Record 6 Set of 4| Victoria
Processing Record 7 Set of 4| Jesus Carranza
Processing Record 8 Set of 4| Yining
City of Yining not found. Skipping...
Processing Record 9 Set of 4| Okhotsk
Processing Record 10 Set of 4| Beringovskiy
Processing Record 11 Set of 4| Provideniya
Processing Record 12 Set of 4| Port-Cartier
Processing Record 13 Set of 4| Luwingu
Processing Record 14 Set of 4| Hobart
Processing Record 15 Set of 4| Praya
Processing Record 16 Set of 4| Ribeira Grande
Processing Record 17 Set of 4| Alta Floresta
Processing Record 18 Set of 4| Mehamn
Processing Record 19 Set of 4| Veshenskaya
Processing Record 20 Set of 4| Petatlan
Processing Record 21 Set of 4| Ayagoz
Processing Record 22 Set of 4| Havre-Saint-Pierre
Processing Record 23 Set of 4| Cabo San Lucas
Processing Record 24 Set of 4| Bani Walid
Processing Record 25 Set of 4| Tekeli
Processing Record 26 Set of 4| Humaita
Processing Record 27 Set of 4| Nagua
Processing Record 28 Set of 4| Tula
Processing Record 29 Set of 4| San Felipe
Processing Record 30 Set of 4| Kailua
Processing Record 31 Set of 4| Sao Joao da Barra
Processing Record 32 Set of 4| Rosetta
Processing Record 33 Set of 4| San Cristobal
Processing Record 34 Set of 4| Half Moon Bay
Processing Record 35 Set of 4| Tortoli
Processing Record 36 Set of 4| Vila
Processing Record 37 Set of 4| Saint-Augustin
Processing Record 38 Set of 4| Luwuk
Processing Record 39 Set of 4| Severo-Kurilsk
Processing Record 40 Set of 4| Labuhan
Processing Record 41 Set of 4| Nouadhibou
Processing Record 42 Set of 4| Dwarka
Processing Record 43 Set of 4| Sitka
Processing Record 44 Set of 4| Kysyl-Syr
Processing Record 45 Set of 4| Bethel
Processing Record 46 Set of 4| Hovd
Processing Record 47 Set of 4| Hithadhoo
Processing Record 48 Set of 4| Natal
Processing Record 49 Set of 4| Praia
Processing Record 50 Set of 4| Vardo
Processing Record 1 Set of 5| Mackay
Processing Record 2 Set of 5| Raahe
Processing Record 3 Set of 5| Maldonado
Processing Record 4 Set of 5| Bandarbeyla
City of Bandarbeyla not found. Skipping...
City of Bandarbeyla not found. Skipping...
Processing Record 5 Set of 5| Mana
Processing Record 6 Set of 5| Tuktoyaktuk
Processing Record 7 Set of 5| Kamennomostskoye
Processing Record 8 Set of 5| Inhambane
Processing Record 9 Set of 5| Puteyets
Processing Record 10 Set of 5| Shingu
Processing Record 11 Set of 5| Hamilton
Processing Record 12 Set of 5| Baracoa
City of Baracoa not found. Skipping...
Processing Record 13 Set of 5| Tilichiki
Processing Record 14 Set of 5| Aripuana
Processing Record 15 Set of 5| Ahuimanu
Processing Record 16 Set of 5| Roebourne
Processing Record 17 Set of 5| Canoinhas
Processing Record 18 Set of 5| Tura
Processing Record 19 Set of 5| Hengyang
Processing Record 20 Set of 5| Mahebourg
City of Mahebourg not found. Skipping...
Processing Record 21 Set of 5| Isangel
Processing Record 22 Set of 5| Kaitangata
City of Kaitangata not found. Skipping...
Processing Record 23 Set of 5| Chuy
Processing Record 24 Set of 5| Necochea
Processing Record 25 Set of 5| Shetpe
Processing Record 26 Set of 5| Bathsheba
Processing Record 27 Set of 5| Mpika
Processing Record 28 Set of 5| Katangi
Processing Record 29 Set of 5| Chapais
Processing Record 30 Set of 5| Pitelino
Processing Record 31 Set of 5| Betanzos
Processing Record 32 Set of 5| Mattru
Processing Record 33 Set of 5| Laguna
Processing Record 34 Set of 5| Santa Maria
Processing Record 35 Set of 5| Palampur
Processing Record 36 Set of 5| Erenhot
Processing Record 37 Set of 5| Aksu
Processing Record 38 Set of 5| Husavik
Processing Record 39 Set of 5| Sayanogorsk
Processing Record 40 Set of 5| Bull Savanna
Processing Record 41 Set of 5| Mount Isa
Processing Record 42 Set of 5| Normandin
Processing Record 43 Set of 5| Shenjiamen
Processing Record 44 Set of 5| Aswan
City of Aswan not found. Skipping...
Processing Record 45 Set of 5| Tiznit
Processing Record 46 Set of 5| Mpongwe
Processing Record 47 Set of 5| Torbay
Processing Record 48 Set of 5| Pilot Butte
Processing Record 49 Set of 5| Udachnyy
Processing Record 50 Set of 5| Dinard
Processing Record 1 Set of 6| Nara
Processing Record 2 Set of 6| College
City of College not found. Skipping...
Processing Record 3 Set of 6| Bako
Processing Record 4 Set of 6| Surgut
Processing Record 5 Set of 6| La Ronge
City of La Ronge not found. Skipping...
Processing Record 6 Set of 6| Kantunilkin
Processing Record 7 Set of 6| Barcelona
Processing Record 8 Set of 6| Puerto Carreno
Processing Record 9 Set of 6| Vammala
Processing Record 10 Set of 6| Vila Velha
Processing Record 11 Set of 6| Milkovo
Processing Record 12 Set of 6| Ballina
Processing Record 13 Set of 6| Leningradskiy
Processing Record 14 Set of 6| Paracambi
Processing Record 15 Set of 6| Rabaul
City of Rabaul not found. Skipping...
Processing Record 16 Set of 6| San Rafael
Processing Record 17 Set of 6| Mayo
Processing Record 18 Set of 6| Balaipungut
Processing Record 19 Set of 6| Ostrovnoy
Processing Record 20 Set of 6| Gulf Gate Estates
Processing Record 21 Set of 6| Mogzon
Processing Record 22 Set of 6| Samagaltay
Processing Record 23 Set of 6| Cockburn Town
Processing Record 24 Set of 6| Porosozero
Processing Record 25 Set of 6| Vao
Processing Record 26 Set of 6| Fairbanks
Processing Record 27 Set of 6| Praia da Vitoria
Processing Record 28 Set of 6| Soe
Processing Record 29 Set of 6| Pozo Colorado
Processing Record 30 Set of 6| Lavrentiya
Processing Record 31 Set of 6| Whitehorse
City of Whitehorse not found. Skipping...
Processing Record 32 Set of 6| Jizan
Processing Record 33 Set of 6| Mirnyy
Processing Record 34 Set of 6| Ukiah
Processing Record 35 Set of 6| Hami
Processing Record 36 Set of 6| Russell
Processing Record 37 Set of 6| San Patricio
City of San Patricio not found. Skipping...
Processing Record 38 Set of 6| Guilin
City of Guilin not found. Skipping...
Processing Record 39 Set of 6| Banda Aceh
Processing Record 40 Set of 6| Hay River
Processing Record 41 Set of 6| Banjar
Processing Record 42 Set of 6| Sorland
Processing Record 43 Set of 6| Tiksi
Processing Record 44 Set of 6| Martos
Processing Record 45 Set of 6| Mildura
Processing Record 46 Set of 6| Inirida
Processing Record 47 Set of 6| Tual
Processing Record 48 Set of 6| Saint George
City of Saint George not found. Skipping...
Processing Record 49 Set of 6| Bosaso
Processing Record 50 Set of 6| Lar
City of Lar not found. Skipping...
City of Lar not found. Skipping...
Processing Record 1 Set of 7| Lasa
Processing Record 2 Set of 7| Beba
Processing Record 3 Set of 7| Port Elizabeth
Processing Record 4 Set of 7| Jalingo
City of Jalingo not found. Skipping...
City of Jalingo not found. Skipping...
City of Jalingo not found. Skipping...
Processing Record 5 Set of 7| Korcula
Processing Record 6 Set of 7| Sao Filipe
Processing Record 7 Set of 7| Lorengau
City of Lorengau not found. Skipping...
Processing Record 8 Set of 7| Creel
Processing Record 9 Set of 7| Pindobacu
Processing Record 10 Set of 7| Jamundi
Processing Record 11 Set of 7| Marsa Matruh
Processing Record 12 Set of 7| Khani
Processing Record 13 Set of 7| Bilma
Processing Record 14 Set of 7| Curuguaty
Processing Record 15 Set of 7| Amuntai
Processing Record 16 Set of 7| Portachuelo
City of Portachuelo not found. Skipping...
Processing Record 17 Set of 7| Taltal
City of Taltal not found. Skipping...
Processing Record 18 Set of 7| Coquimbo
Processing Record 19 Set of 7| Kingman
Processing Record 20 Set of 7| Nampa
Processing Record 21 Set of 7| Verkhoyansk
Processing Record 22 Set of 7| Samarai
Processing Record 23 Set of 7| Bonthe
Processing Record 24 Set of 7| Alghero
City of Alghero not found. Skipping...
Processing Record 25 Set of 7| Dali
Processing Record 26 Set of 7| Aquiraz
Processing Record 27 Set of 7| Aklavik
Processing Record 28 Set of 7| Malanville
Processing Record 29 Set of 7| Horn Lake
Processing Record 30 Set of 7| Rawson
Processing Record 31 Set of 7| Winnemucca
Processing Record 32 Set of 7| Kalmunai
Processing Record 33 Set of 7| Porto Novo
Processing Record 34 Set of 7| Talnakh
Processing Record 35 Set of 7| Chumikan
Processing Record 36 Set of 7| Stromness
Processing Record 37 Set of 7| Leiyang
Processing Record 38 Set of 7| Te Anau
Processing Record 39 Set of 7| Mercedes
Processing Record 40 Set of 7| Patacamaya
Processing Record 41 Set of 7| Walvis Bay
Processing Record 42 Set of 7| Tuatapere
Processing Record 43 Set of 7| Richards Bay
Processing Record 44 Set of 7| Qaqortoq
Processing Record 45 Set of 7| Boguchany
Processing Record 46 Set of 7| Upernavik
Processing Record 47 Set of 7| Shenzhen
Processing Record 48 Set of 7| Beian
Processing Record 49 Set of 7| Taldan
Processing Record 50 Set of 7| Buraydah
Processing Record 1 Set of 8| Carai
City of Carai not found. Skipping...
Processing Record 2 Set of 8| Norman Wells
Processing Record 3 Set of 8| Noyabrsk
Processing Record 4 Set of 8| Saran
Processing Record 5 Set of 8| Ancud
Processing Record 6 Set of 8| Kishtwar
Processing Record 7 Set of 8| Jalu
City of Jalu not found. Skipping...
Processing Record 8 Set of 8| Slonim
Processing Record 9 Set of 8| Klaksvik
City of Klaksvik not found. Skipping...
Processing Record 10 Set of 8| Tazovskiy
Processing Record 11 Set of 8| Lorut
Processing Record 12 Set of 8| Yinchuan
Processing Record 13 Set of 8| Tsabong
Processing Record 14 Set of 8| Haapiti
Processing Record 15 Set of 8| Baijiantan
Processing Record 16 Set of 8| Preeceville
Processing Record 17 Set of 8| Voi
Processing Record 18 Set of 8| Kurchum
Processing Record 19 Set of 8| Juneau
Processing Record 20 Set of 8| Lakes Entrance
Processing Record 21 Set of 8| Ust-Kuyga
Processing Record 22 Set of 8| Eskisehir
Processing Record 23 Set of 8| Hasaki
Processing Record 24 Set of 8| Gornopravdinsk
Processing Record 25 Set of 8| Huntsville
Processing Record 26 Set of 8| Haines Junction
Processing Record 27 Set of 8| Kenai
Processing Record 28 Set of 8| Mtsamboro
Processing Record 29 Set of 8| Nicolas Bravo
Processing Record 30 Set of 8| Basco
Processing Record 31 Set of 8| Kamiiso
Processing Record 32 Set of 8| Bubaque
Processing Record 33 Set of 8| Octeville
Processing Record 34 Set of 8| Santa Isabel do Rio Negro
Processing Record 35 Set of 8| Grand Gaube
Processing Record 36 Set of 8| Nelson Bay
Processing Record 37 Set of 8| Dickinson
Processing Record 38 Set of 8| Hambantota
Processing Record 39 Set of 8| Pringsewu
Processing Record 40 Set of 8| Kandrian
Processing Record 41 Set of 8| Sobolevo
Processing Record 42 Set of 8| Xianshuigu
Processing Record 43 Set of 8| Abu Dhabi
Processing Record 44 Set of 8| Zwevegem
Processing Record 45 Set of 8| Hobyo
Processing Record 46 Set of 8| Rio Grande
Processing Record 47 Set of 8| Taoudenni
Processing Record 48 Set of 8| Dera Bugti
Processing Record 49 Set of 8| Saint-Pierre
Processing Record 50 Set of 8| Katsuura
Processing Record 1 Set of 9| Arys
Processing Record 2 Set of 9| Belem de Sao Francisco
Processing Record 3 Set of 9| Salalah
Processing Record 4 Set of 9| Socorro
Processing Record 5 Set of 9| Porkhov
Processing Record 6 Set of 9| Atherton
Processing Record 7 Set of 9| Kiama
City of Kiama not found. Skipping...
Processing Record 8 Set of 9| Rjukan
Processing Record 9 Set of 9| Nyagan
Processing Record 10 Set of 9| Nanakuli
Processing Record 11 Set of 9| Jacobina
Processing Record 12 Set of 9| Bonfim
Processing Record 13 Set of 9| Macau
Processing Record 14 Set of 9| Ewa Beach
City of Ewa Beach not found. Skipping...
Processing Record 15 Set of 9| San Quintin
Processing Record 16 Set of 9| Saldanha
Processing Record 17 Set of 9| Dzhebariki-Khaya
Processing Record 18 Set of 9| Los Andes
Processing Record 19 Set of 9| Sao Jose de Ribamar
Processing Record 20 Set of 9| Padang
Processing Record 21 Set of 9| Calvia
Processing Record 22 Set of 9| Presidencia Roque Saenz Pena
Processing Record 23 Set of 9| Grants
Processing Record 24 Set of 9| Melioratorov
Processing Record 25 Set of 9| Ojinaga
Processing Record 26 Set of 9| Moree
City of Moree not found. Skipping...
Processing Record 27 Set of 9| Harper
Processing Record 28 Set of 9| Jijiga
Processing Record 29 Set of 9| Gallup
City of Gallup not found. Skipping...
Processing Record 30 Set of 9| Ust-Kut
Processing Record 31 Set of 9| Bhojudih
Processing Record 32 Set of 9| Benguela
Processing Record 33 Set of 9| Sola
Processing Record 34 Set of 9| Dingle
Processing Record 35 Set of 9| Priyutovo
Processing Record 36 Set of 9| Santa Maria del Oro
Processing Record 37 Set of 9| Westport
Processing Record 38 Set of 9| Port Blair
Processing Record 39 Set of 9| Lezajsk
Processing Record 40 Set of 9| Harduaganj
Processing Record 41 Set of 9| Geraldton
Processing Record 42 Set of 9| Quincy
City of Quincy not found. Skipping...
Processing Record 43 Set of 9| Golaghat
Processing Record 44 Set of 9| Nikolayevskaya
Processing Record 45 Set of 9| Olinda
Processing Record 46 Set of 9| Batagay
Processing Record 47 Set of 9| Polunochnoye
Processing Record 48 Set of 9| Dalbandin
Processing Record 49 Set of 9| Saint-Francois
City of Saint-Francois not found. Skipping...
Processing Record 50 Set of 9| Luebo
Processing Record 1 Set of 10| Kedrovyy
Processing Record 2 Set of 10| Pochutla
Processing Record 3 Set of 10| Burley
Processing Record 4 Set of 10| Leh
Processing Record 5 Set of 10| Vitim
Processing Record 6 Set of 10| Santa Rosa
Processing Record 7 Set of 10| Pisco
Processing Record 8 Set of 10| Nouakchott
Processing Record 9 Set of 10| Nishihara
Processing Record 10 Set of 10| Itoman
Processing Record 11 Set of 10| Port Macquarie
Processing Record 12 Set of 10| Coihaique
Processing Record 13 Set of 10| Abancay
Processing Record 14 Set of 10| Porto Walter
Processing Record 15 Set of 10| Dunedin
Processing Record 16 Set of 10| Whitecourt
Processing Record 17 Set of 10| Saravan
Processing Record 18 Set of 10| Amapa
Processing Record 19 Set of 10| Miandrivazo
Processing Record 20 Set of 10| Rio Gallegos
Processing Record 21 Set of 10| Buenaventura
Processing Record 22 Set of 10| Pedregulho
Processing Record 23 Set of 10| Mokhsogollokh
Processing Record 24 Set of 10| Norton
Processing Record 25 Set of 10| Kruisfontein
Processing Record 26 Set of 10| Kahului
Processing Record 27 Set of 10| Gardez
City of Gardez not found. Skipping...
Processing Record 28 Set of 10| Rocky Mount
Processing Record 29 Set of 10| Gazanjyk
Processing Record 30 Set of 10| Dudinka
Processing Record 31 Set of 10| Karratha
Processing Record 32 Set of 10| San Buenaventura
Processing Record 33 Set of 10| Belawan
Processing Record 34 Set of 10| Sayyan
Processing Record 35 Set of 10| Niteroi
Processing Record 36 Set of 10| Ngunguru
Processing Record 37 Set of 10| Lethem
Processing Record 38 Set of 10| Plettenberg Bay
Processing Record 39 Set of 10| Kabompo
Processing Record 40 Set of 10| Douglas
Processing Record 41 Set of 10| Coronado
Processing Record 42 Set of 10| Zonguldak
Processing Record 43 Set of 10| Toora-Khem
Processing Record 44 Set of 10| Tuskegee
Processing Record 45 Set of 10| Kommunar
Processing Record 46 Set of 10| Terrasini
Processing Record 47 Set of 10| Kamenka
Processing Record 48 Set of 10| Stephenville
Processing Record 49 Set of 10| Sisophon
Processing Record 50 Set of 10| Synya
-----------------------
Data Retrieval Complete
-----------------------

Convert Raw Data to DataFrame
weather_dict = {
    "city": CityName,
    "Cloudiness": Cloudiness,
    "Country": Country,
    "Date": Date_Info,
    "Humidity": Humidity,
    "lat": lat,
    "lon": lon,
    "Max Temp": MaxT,
    "Wind Speed": MaxW
}

weather_info = pd.DataFrame(weather_dict)

# Make sure consistency in each data exist with count 
weather_info.count()
city          500
Cloudiness    500
Country       500
Date          500
Humidity      500
lat           500
lon           500
Max Temp      500
Wind Speed    500
dtype: int64

# Save Data to csv
weather_info.to_csv(output_data_file)

weather_info.head()

city	Cloudiness	Country	Date	Humidity	lat	lon	Max Temp	Wind Speed
0	Aksarayskiy	0	RU	1570268215	28	46.79	48.01	23.00	8.00
1	New Norfolk	40	AU	1570268217	62	-42.78	147.06	12.00	3.60
2	Marzuq	12	YE	1570268219	15	14.40	46.47	31.31	6.82
3	Rikitea	100	PF	1570268221	81	-23.12	-134.97	21.01	9.86
4	East London	20	ZA	1570268222	57	-33.02	27.91	24.00	6.70

Plotting the Data

Latitude vs. Temperature Plot
# Build a scatter plot for each data type
plt.scatter(weather_info["lat"], weather_info["Max Temp"], marker="o")

# Incorporate the other graph properties
plt.title("Temperature in World Cities")
plt.ylabel("Temperature (Celsius)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("TemperatureInWorldCities.png")

# Show plot
plt.show()

Latitude vs. Humidity Plot
# Build a scatter plot for each data type
plt.scatter(weather_info["lat"], weather_info["Humidity"], marker="o")

# Incorporate the other graph properties
plt.title("Humidity in World Cities")
plt.ylabel("Temperature (Percentage)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("HumidityInWorldCities.png")

# Show plot
plt.show()

Latitude vs. Cloudiness Plot
# Build a scatter plot for each data type
plt.scatter(weather_info["lat"], weather_info["Cloudiness"], marker="o")

# Incorporate the other graph properties
plt.title("Cloudiness in World Cities")
plt.ylabel("Cloudiness (Percentage)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("CloudinessInWorldCities.png")

# Show plot
plt.show()

Latitude vs. Wind Speed Plot
# Build a scatter plot for each data type
plt.scatter(weather_info["lat"], weather_info["Wind Speed"], marker="o")

# Incorporate the other graph properties
plt.title("Wind Speed in World Cities")
plt.ylabel("Wind Speedper (KPH)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("WindSpeedInWorldCities.png")

# Show plot
plt.show()
