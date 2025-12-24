# Ex.04 Design a Website for Server Side Processing
## Date:

## AIM:
 To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side. 


## FORMULA:
P = I<sup>2</sup>R
<br> P --> Power (in watts)
<br> I --> Intensity
<br> R --> Resistance

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
```
bmi_calculator.html
<!DOCTYPE html>
<html>
<head>
    <title>BMI Calculator</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        form {
            width: 300px;
            padding: 20px;
            border: 1px solid #888;
            border-radius: 8px;
            margin-left: 50%;
            transform: translateX(-50%);
        }
        input { width: 100%; margin: 10px 0; padding: 8px; }
        .result { margin-top: 20px; padding: 10px; background: #f1f1f1; }
    </style>
</head>

<body>
    <h2 align="center">BMI Calculator (Server-side in Django)</h2>

    <form method="POST">
        {% csrf_token %}
        <label>Weight (kg)</label>
        <input type="number" step="0.1" name="weight" required>

        <label>Height (cm)</label>
        <input type="number" step="0.1" name="height" required>

        <button type="submit">Calculate BMI</button>
        {% if bmi %}
        <div class="result">
            <strong>Your BMI:</strong> {{ bmi }}<br>
            <strong>Category:</strong> {{ category }}
        </div>
        {% endif %}
    </form>

    
</body>
</html>

views.py
from django.shortcuts import render

# Create your views here.
def bmi_calculator(request):
    bmi = None
    category = None

    if request.method == "POST":
        weight = float(request.POST.get("weight"))
        height = float(request.POST.get("height"))

        # Convert height from cm to meters
        height_m = height / 100

        # BMI formula
        bmi = weight / (height_m ** 2)
        bmi = round(bmi, 2)

        # Classification
        if bmi < 18.5:
            category = "Underweight"
        elif 18.5 <= bmi < 24.9:
            category = "Normal weight"
        elif 25 <= bmi < 29.9:
            category = "Overweight"
        else:
            category = "Obesity"

    return render(request, "bmi_calculator.html", {
        "bmi": bmi,
        "category": category
    })

urls.py
from django.contrib import admin
from django.urls import path
from BMI_app import views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('bmi', views.bmi_calculator, name='bmi'),
]
```

## SERVER SIDE PROCESSING:
<img width="1031" height="544" alt="529862497-48321c02-7007-4ac7-9670-95cacf411b1f" src="https://github.com/user-attachments/assets/1cb2e440-c4f7-4b24-a946-56fd2b0db5f2" />


## HOMEPAGE:
<img width="1039" height="528" alt="529862543-2b9506e0-b1f3-4b7e-bf20-71d9f6d61c78" src="https://github.com/user-attachments/assets/8a6f68ae-6cde-4c44-8832-d562a98b20f3" />


## RESULT:
The program for performing server side processing is completed successfully.
