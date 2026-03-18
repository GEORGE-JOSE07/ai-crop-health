# --- STEP 1: Create the Mask (The Brain) ---
mask = cv2.inRange(hsv, lower_green, upper_green)

# --- STEP 2: Add your Severity Code here (The Math) ---
# This counts how many pixels are NOT green (stressed/bare soil)
stressed_pixels = np.sum(mask == 0) 
total_pixels = mask.size
severity_score = (stressed_pixels / total_pixels) * 100

# --- STEP 3: Use the Score (The Action) ---
# Now you can use 'severity_score' to show a message or change colors
if severity_score > 50:
    print(f"ALERT: High Stress Detected! Score: {severity_score:.2f}%")
else:
    print(f"Field is Healthy. Score: {severity_score:.2f}%")

# --- STEP 4: Display the Image (The Visual) ---
cv2.imshow('Health Map', health_map)
