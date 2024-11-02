# showing-the-code-snippet-for-LIST-ALL-LIST-BY-NAME-LIST-BY-CATEGORY-and-LIST-BY-AVAILABILITY-fun.
@app.route("/products", methods=["GET"])
def list_products():
    name = request.args.get("name")
    category = request.args.get("category")
    available = request.args.get("available")
    
    # Filter based on query parameters
    products = Product.query
    if name:
        products = products.filter_by(name=name)
    if category:
        products = products.filter_by(category=category)
    if available:
        products = products.filter_by(available=(available.lower() == 'true'))
    
    products = products.all()
    return jsonify([product.serialize() for product in products]), 200
