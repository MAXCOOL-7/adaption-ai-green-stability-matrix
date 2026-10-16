# adaption-ai-green-stability-matrix
Automated carbon lifecycle auditing system and eco-intelligence platform for e-commerce catalogs (Build54 Hackathon).
# 🌿 Adaption AI • Green Stability Matrix
> *Transforming E-Commerce Through Adaptive Intelligence & Catalog Carbon Auditing*

**Adaption AI Green Stability Matrix** is an automated carbon lifecycle auditing system designed for modern e-commerce stores. Built for the Build54 hackathon (focusing on "Best Use of Adaption AI"), this project demonstrates how AI can empower merchants and shoppers to measure, verify, and reduce $\text{CO}_2$ emissions across online stores—scaling seamlessly from apparel and accessories to edible goods.

---

## 🚀 Live Store Demonstration
* **Target Store:** HOOD-BOSS (Shopify - Horizon Theme)
* **Core Offerings:** Sustainable streetwear, caps, beanies, and eco-efficient hoodies.
* **Live Features:** Product carbon audit rating badges, Green Stability Index percentages, lowest-footprint picks grid, and cart carbon-neutral pledges.

---

## 🛠️ Tech Stack & ML/Dev
* **Frontend / E-Commerce:** Shopify (Horizon Theme), Custom Liquid, Tailwind CSS, JavaScript.
* **Backend / ML Pipeline:** Python, FastAPI, automated CSV data normalization, custom ML/AI scoring endpoints.
* **AI & Intelligence:** Adaption AI (Adaptive Data pipeline & AutoScientist domain fine-tuning).

---

## 🌟 Key Features
* **Real-Time Product Auditing:** Instantly calculates estimated kg $\text{CO}_2\text{e}$ and assigns an A+ to D rating badge to items.
* **Cross-Category Scalability:** Architecture built to handle apparel, physical accessories, and sensitive edible product supply chains.
* **Frictionless Integration:** Drop-in Custom Liquid blocks requiring zero heavy third-party app installations.
* **Empowered Buyers & Sellers:** Bridges customer awareness at checkout with strict merchant catalog standards.

---

## 💻 Core Code Components

### 1. The Cart/Checkout Carbon Neutral Pledge (`cart-eco-pledge.liquid`)
Allows customers to voluntarily opt-in to fund verified reforestation projects directly from the cart drawer before checkout.

```html
<div class="p-4 my-4 bg-emerald-50/60 border border-emerald-500/30 rounded-xl font-sans shadow-sm">
  <div class="flex items-center justify-between mb-2">
    <span class="text-xs font-bold uppercase tracking-wider text-emerald-900 flex items-center gap-1">🌱 Adaption AI • Carbon Neutral Pledge</span>
    <span class="px-2 py-0.5 text-xs font-bold text-emerald-800 bg-emerald-100 rounded-full">Zero-Net Goal</span>
  </div>
  <p class="text-xs text-stone-600 mb-3">Opt-in to neutralize your order's estimated carbon footprint via verified reforestation projects.</p>
  
  <label class="flex items-center gap-3 p-3 bg-white rounded-lg border border-emerald-500/20 cursor-pointer hover:bg-emerald-50/30 transition">
    <input type="checkbox" id="eco-offset-toggle" class="w-4 h-4 text-emerald-600 rounded border-stone-300 focus:ring-emerald-500" onchange="toggleEcoOffset(this)">
    <div class="text-xs">
      <span class="font-bold text-stone-900 block">Add $0.50 Green Offset Pledge</span>
      <span class="text-stone-500">Funds local tree planting to offset this order's $\text{CO}_2$ output.</span>
    </div>
  </label>
</div>

<script>
function toggleEcoOffset(checkbox) {
  const isChecked = checkbox.checked;
  fetch('/cart/update.js', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      attributes: { "Carbon Neutral Offset Pledged": isChecked ? "Yes ($0.50 Added)" : "No" }
    })
  }).then(() => {
    console.log("Adaption AI Offset updated:", isChecked);
  });
}
</script>

2. Seller Green-Standard Validator (green_validator.py)
Ensures that merchants and suppliers tag items with certified green materials and adhere to weight-efficiency thresholds before publishing products.
def validate_seller_product(product_title, material_tag, weight_kg):
    allowed_materials = ["organic-cotton", "recycled-poly", "canvas", "wool"]
    
    is_material_green = material_tag.lower() in allowed_materials
    is_weight_efficient = weight_kg <= 0.8  # Flags excessive heavy synthetic waste
    
    if is_material_green and is_weight_efficient:
        return {
            "status": "APPROVED",
            "message": f"'{product_title}' meets HOOD-BOSS green standards. AutoScientist checkpoint updated."
        }
    else:
        return {
            "status": "REJECTED_FOR_REVIEW",
            "message": f"'{product_title}' failed green verification. Material must be organic/recycled and under 0.8kg."
        }

# Example validation test
print(validate_seller_product("Prospector Graphic Hoodie", "organic-cotton", 0.65))
