import os
from flask import Flask, request, jsonify
from flask_cors import CORS
import ddddocr
import base64

app = Flask(__name__)
CORS(app)
ocr = ddddocr.DdddOcr(show_ad=False)

@app.route('/ocr', methods=['POST'])
def do_ocr():
    try:
        data = request.json['image'].split(',')[1]
        img_bytes = base64.b64decode(data)
        res = ocr.classification(img_bytes)
        return jsonify({"result": res})
    except Exception as e:
        return jsonify({"error": str(e)}), 400

if __name__ == "__main__":
    # Render 會自動分配 PORT
    port = int(os.environ.get("PORT", 5000))
    app.run(host='0.0.0.0', port=port)
