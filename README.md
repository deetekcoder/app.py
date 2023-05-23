from flask import Flask, jsonify
from bs4 import BeautifulSoup
import requests

app = Flask(__name__)

@app.route('/price', methods=['GET'])
def get_price():
    try:
        url = "https://www.metal.com/Lithium-ion-Battery/202303240001"
        response = requests.get(url)
        response.raise_for_status()
        soup = BeautifulSoup(response.content, 'html.parser')
        price_element = soup.find("span", class_="price")
        price = price_element.text.strip() if price_element else "Price not found"
        return jsonify(price=price)
    except requests.exceptions.RequestException as e:
        return jsonify(error=str(e)), 500
    except Exception as e:
        return jsonify(error="An error occurred"), 500

if __name__ == '__main__':
    app.run()
