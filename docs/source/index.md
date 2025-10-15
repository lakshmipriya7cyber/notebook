# Sample Health Mirror 360 program

def calculate_health_score(data):
    """
    Calculate health score out of 100 based on lifestyle data.
    Simple weighted scoring for demo purposes.
    """
    score = 0
    
    # Sleep: ideal 7-9 hours
    if 7 <= data['sleep_hours'] <= 9:
        score += 30
    elif 5 <= data['sleep_hours'] < 7 or 9 < data['sleep_hours'] <= 10:
        score += 20
    else:
        score += 10
    
    # Steps: ideal 7000+
    if data['steps_walked'] >= 7000:
        score += 30
    elif 4000 <= data['steps_walked'] < 7000:
        score += 20
    else:
        score += 10
    
    # Water intake (liters): ideal 2-3 liters
    if 2 <= data['water_intake'] <= 3:
        score += 30
    elif 1.5 <= data['water_intake'] < 2 or 3 < data['water_intake'] <= 3.5:
        score += 20
    else:
        score += 10
    
    # Diet notes simple check for "healthy" keyword
    if 'healthy' in data['diet_notes'].lower():
        score += 10
    else:
        score += 5
    
    # Normalize score to 100 max (max could be 100+10)
    if score > 100:
        score = 100
    
    return score

def generate_tips(data):
    """
    Generate 1-3 tips based on user's lifestyle data.
    """
    tips = []
    
    if data['sleep_hours'] < 7:
        tips.append("Try to sleep more hours")
    elif data['sleep_hours'] > 9:
        tips.append("Avoid oversleeping")
    
    if data['steps_walked'] < 7000:
        tips.append("Walk extra steps today")
    
    if data['water_intake'] < 2:
        tips.append("Drink more water")
    
    if 'healthy' not in data['diet_notes'].lower():
        tips.append("Include more healthy foods")
    
    # Return up to 3 tips
    return tips[:3]

def color_code(score):
    """
    Return color code string based on score.
    """
    if score >= 75:
        return "Green (Good)"
    elif score >= 50:
        return "Yellow (Average)"
    else:
        return "Red (Needs Improvement)"

def main():
    # Sample user input data
    user_data = {
        'sleep_hours': float(input("Enter sleep hours last night: ")),
        'steps_walked': int(input("Enter steps walked today: ")),
        'water_intake': float(input("Enter water intake (liters): ")),
        'diet_notes': input("Enter any notes about your diet: "),
    }
    
    score = calculate_health_score(user_data)
    tips = generate_tips(user_data)
    color = color_code(score)
    
    # Output
    tips_text = ", ".join(tips) if tips else "Keep up the good work!"
    print(f"\nDaily Health Score: {score} ({color})")
    print(f"Tips: {tips_text}")

if name == "main":
    main()
    
