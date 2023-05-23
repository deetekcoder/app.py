# app.py
from flask import Flask, jsonify
from bs4 import BeautifulSoup
import requests

app = Flask(__name__)

@app.route('/price', methods=['GET'])
def get_price():
    url = 'https://www.metal.com/Lithium-ion-Battery/202303240001'
    try:
        response = requests.get(url)
        response.raise_for_status()
        soup = BeautifulSoup(response.text, 'html.parser')
        # Perform web scraping to extract the latest price from the webpage
        # Extract the necessary information and store it in a variable, e.g., price
        price = extract_price(soup)
        return jsonify({'price': price})
    except requests.exceptions.RequestException as e:
        # Handle any errors that occurred during the request or scraping
        return jsonify({'error': str(e)}), 500

def extract_price(soup):
    # Implement the logic to extract the price from the BeautifulSoup object
    # Return the extracted price
    pass

FLASK_APP=app.py flask run
