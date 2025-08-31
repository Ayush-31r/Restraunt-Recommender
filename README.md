# 🍽️ Predictive Restaurant Recommender

## 🧠 Problem Statement
The objective of this project is to predict **which vendor a customer is most likely to order from** by leveraging customer and location information along with historical purchase behavior.  
The prediction is framed as a **classification task** over all possible `(customer, location, vendor)` triples.

---

## 📁 Dataset Overview

### 🔹 Training Data
- **`train_customers.csv`** → `customer_id`, `gender`, `age`, `location_number`  
- **`train_locations.csv`** → `location_number`, `location_type`, `coordinates`  
- **`orders.csv`** → past order history mapping customers to vendors  
- **`vendors.csv`** → vendor details and associated location info  

### 🔹 Test Data
- **`test_customers.csv`** and **`test_locations.csv`** (same structure as training counterparts)  
- Vendor information and labels are withheld for prediction.  

---

## ⚙️ Workflow

### 1. **Data Assembly**
- Integrated customer, location, vendor, and order data into a unified training view.  

### 2. **Feature Engineering**
- Selected attributes: `gender`, `location_type`, `latitude`, `longitude`.  
- Dropped `age` due to high missingness.  
- Applied **Label Encoding** for categorical columns.  

### 3. **Training Set Construction**
- Generated **all possible combinations** of `(customer, location)` with every vendor (via cross join).  
- Created the binary label (`target`) by marking vendors a customer has ordered from as `1`, others as `0`.  

### 4. **Modeling**
- Used **XGBoost Classifier** for prediction.  
- Performance measured with **Accuracy** and **F1-score** on a validation split.  

### 5. **Test Preparation**
- Merged test customers with test locations.  
- Cross-joined with **all vendors** observed in training.  
- Encoded features with the same transformations as training.  
- Generated predictions using the trained model.  

### 6. **Prediction Output**
- Final predictions formatted as:  

---

## 📦 Output Format

| Combination (CID X LOC_NUM X VENDOR) | target |
|--------------------------------------|--------|
| Z59FTQD X 0 X 243                    | 0      |
| 0JP29SK X 1 X 243                    | 1      |
| ...                                  | ...    |

---

## 🛠️ Tools & Libraries
- **Python** (data processing & ML pipeline)  
- **Pandas**, **NumPy** (feature handling & joins)  
- **Scikit-learn** (encoders & validation)  
- **XGBoost** (classification model)  

---

## ✅ Key Takeaways
- Unified representation of data where **each row = one unique (customer, location, vendor) scenario**.  
- Constructed training labels directly from order history.  
- End-to-end pipeline that handles **data integration → feature encoding → model training → prediction → submission formatting**.  
