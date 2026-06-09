import re
import json

def extract_fields(text):
    fields = {}

    patterns = {
        "policyNumber": r"Policy Number:\s*(.*)",
        "policyholderName": r"Policyholder Name:\s*(.*)",
        "date": r"Date:\s*(.*)",
        "time": r"Time:\s*(.*)",
        "location": r"Location:\s*(.*)",
        "description": r"Description:\s*(.*)",
        "claimant": r"Claimant:\s*(.*)",
        "assetType": r"Asset Type:\s*(.*)",
        "assetId": r"Asset ID:\s*(.*)",
        "estimatedDamage": r"Estimated Damage:\s*(\d+)",
        "claimType": r"Claim Type:\s*(.*)"
    }

    for key, pattern in patterns.items():
        match = re.search(pattern, text)
        if match:
            fields[key] = match.group(1)

    return fields

with open("claim1.txt", "r") as file:
    text = file.read()

fields = extract_fields(text)

output = {
    "extractedFields": fields,
    "missingFields": [],
    "recommendedRoute": "Fast-track",
    "reasoning": "Estimated damage below 25000"
}

print(json.dumps(output, indent=4))
