# Intelligent_recipe_recommendation_for_taste_disorder
This proposal outlines a machine learning-based system to recommend personalized recipes for chemotherapy patients experiencing taste disorders. The system leverages a large recipe corpus and patient-specific profiles to address unique dietary needs, aiming to enhance nutritional intake and improve quality of life.

---

## 📖 Abstract

Chemotherapy can alter taste perception, creating unique dietary challenges for patients. This system utilizes a dataset of 500,000 recipes and patient-specific profiles to recommend recipes tailored to individual preferences, symptoms, and dietary restrictions. Strategies such as incorporating strong flavors, using plastic utensils for metallic tastes, and adding texture diversity enhance personalization and the overall eating experience. This repo is mainly created to demonstrate how the algorithm will will work based on the paper given for evealuation.

---

## 🛠 Methodology with Example

### **1. Prepare the Recipe Dataset**
**Example:**
- **Raw Recipe Data:**
  - **Name:** "Grilled Chicken with Vegetables"
  - **Nutritional Content:** Sodium: 120 mg, Protein: 35 g, Fat: 10 g
  - **Ingredients:** ["chicken breast", "bell peppers", "olive oil", "garlic", "salt"]
  - **Instructions:** "Grill the chicken breast with olive oil and garlic. Serve with sautéed vegetables."
  - **Metadata:** Cooking time: 30 minutes.

- **Processed Data:**
  - **Recipe Embedding:** `[0.85 (protein-rich), 0.10 (low-sodium), 0.50 (grilled)]`
  - **Tags:** `["low-sodium", "high-protein", "gluten-free"]`

---

### **2. Generate Dietary Tags for Recipes**
**Example:**
- **Threshold Rules:**
  - Low-sodium: Sodium < 140 mg.
  - High-protein: Protein > 20 g.
  - Gluten-free: No gluten-containing ingredients.

- **Processed Tags for Recipe:**
  - Sodium = 120 mg → "low-sodium"
  - Protein = 35 g → "high-protein"
  - Ingredients contain no gluten → "gluten-free"
  - **Final Tags:** `["low-sodium", "high-protein", "gluten-free"]`

---

### **3. Collect Patient Profiles**
**Example:**
- **Patient Input:**
  - **Name:** "John Doe"
  - **Taste Preferences:** Sweet = 0.2, Salty = 0.5, Bitter = 0.1, Mild = 0.7.
  - **Dietary Needs:** Low-sodium, high-protein.
  - **Symptoms:** Nausea, metallic taste.
  - **Allergies:** Dairy.

- **Patient Profile Encoding:**
  - **Preferences Vector:** `[0.2 (sweet), 0.5 (salty), 0.1 (bitter), 0.7 (mild)]`
  - **Constraints:** `["low-sodium", "high-protein", "dairy-free"]`

---

### **4. Filter Recipes**
**Example:**
- **Filters Applied to the Recipe Dataset:**
  - Remove recipes with allergens (e.g., dairy).
  - Retain recipes with low-sodium and high-protein tags.
  - Exclude recipes with strong flavors (e.g., bitter or highly spiced).

- **Filtered Recipes:**
  - Grilled Chicken with Vegetables (Tags: low-sodium, high-protein, gluten-free)
  - Lentil Soup (Tags: low-sodium, gluten-free)
  - Salmon Salad (Tags: high-protein, dairy-free)

---

### **5. Score and Rank Recipes**
**Example:**
- **Patient Profile Vector:** `[0.2 (sweet), 0.5 (salty), 0.1 (bitter), 0.7 (mild)]`

- **Recipe Embeddings:**
  - Grilled Chicken with Vegetables: `[0.1 (sweet), 0.6 (salty), 0.1 (bitter), 0.8 (mild)]`
  - Lentil Soup: `[0.3 (sweet), 0.4 (salty), 0.2 (bitter), 0.6 (mild)]`
  - Salmon Salad: `[0.2 (sweet), 0.5 (salty), 0.1 (bitter), 0.7 (mild)]`

- **Cosine Similarity Scores:**
  - Grilled Chicken: 0.96
  - Lentil Soup: 0.85
  - Salmon Salad: 0.99

- **Ranked Recipes:**
  - 1st: Salmon Salad
  - 2nd: Grilled Chicken with Vegetables
  - 3rd: Lentil Soup

---

### **6. Generate Final Recommendations**
**Example:**
- **Top Recommendations (Displayed on Web App):**
  - **Salmon Salad**
    - Nutritional Info: Protein: 40 g, Sodium: 90 mg.
    - Tags: High-protein, Dairy-free.
    - Preparation Time: 20 minutes.

  - **Grilled Chicken with Vegetables**
    - Nutritional Info: Protein: 35 g, Sodium: 120 mg.
    - Tags: Low-sodium, High-protein, Gluten-free.
    - Preparation Time: 30 minutes.

---

### **7. Deliver Recipes via Web Application**
**Example:**
- **Displayed Recipe Card (Salmon Salad):**
  ```yaml
  Recipe: Salmon Salad
  Tags: High-protein, Dairy-free
  Prep Time: 20 minutes
  Nutritional Info: Protein: 40g, Sodium: 90mg
  Instructions: Mix salmon with fresh greens, olive oil, and lemon juice.
