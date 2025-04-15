import requests
import pandas as pd

# API anahtarın ve seri ID
api_key = '................'  #FRED anahtarı
series_id = 'WUITUR'    # çekilecek veri
start_date = '2010-01-01'    # başlangıç tarihi 

# API URL'si
url = f'https://api.stlouisfed.org/fred/series/observations?series_id={series_id}&api_key={api_key}&file_type=json&observation_start={start_date}'

# API isteği
response = requests.get(url)
data = response.json()

# JSON'u pandas DataFrame'e çevir
df = pd.DataFrame(data['observations'])

# Tarih ve değer sütunlarını işle
df['date'] = pd.to_datetime(df['date'])
df['value'] = pd.to_numeric(df['value'], errors='coerce')

# İlk 5 satırı göster
print(df.head())
