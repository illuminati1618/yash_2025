---
layout: page
title: Starting the PPR off
description: My introduction to the PPR and what I plan to do in the future.
course: "compsci"
week: 23
type: hacks
comments: true
---

## Requirement 1: A Procedure with Parameters, Selection, and Iteration

### The Procedure Definition:

```python
@token_required()
def put(self):
    """
    Update and add to the interests of the authenticated user.
    """
    current_user = g.current_user
    user = User.query.filter_by(_uid=current_user.uid).first()
    if not user:
        return {'message': 'User not found'}, 404

    body = request.get_json()
    new_interests = body.get('interests')
    if not new_interests:
        return {'message': 'No new interests provided'}, 400

    formatted_new_interests = re.sub(r'\s*,\s*', ', ', new_interests.strip())
    current_interests = user.interests.split(', ') if user.interests else []
    new_interests_list = formatted_new_interests.split(', ')
    
    combined_interests = current_interests.copy()
    for interest in new_interests_list:
        if interest not in combined_interests:
            combined_interests.append(interest)
    
    user.interests = ', '.join(combined_interests)
    user.update({'interests': user.interests})
    return jsonify(user.interests)
```

This procedure is pretty cool because:

- It has a clear name (`put`) and returns JSON data
- It takes in parameters like the current user and the request body
- It follows a sequence of steps to process the interests
- It uses if-statements to check for errors (that's the selection part)
- It does iteration when it splits strings, combines lists, and joins them back together

Basically, it lets users update their interests without creating duplicates.

## Requirement 2: Where the Procedure Gets Called

### The Function Call:

```javascript
async function editInterest(oldInterest) {
    const newInterest = prompt("Edit interest:", oldInterest);
    if (newInterest && newInterest.trim() !== "") {
        try {
            // Delete the old interest
            await fetch(pythonURI + "/api/interests", {
                ...fetchOptions,
                method: 'DELETE',
                body: JSON.stringify({ interest: oldInterest })
            });

            // Add the new interest
            const response = await fetch(pythonURI + "/api/interests", {
                ...fetchOptions,
                method: 'PUT',
                body: JSON.stringify({ interests: newInterest })
            });

            if (!response.ok) {
                throw new Error('Failed to edit interest');
            }

            showError('Interest edited successfully', 'green');
            updateUserInfo();
        } catch (error) {
            console.error('Error editing interest:', error);
            showError('Error editing interest');
        }
    }
}
```

This JavaScript function:
- Asks the user for a new interest name
- Makes a PUT request to our API (this is where it calls our Python procedure!)
- Sends the new interest in the request body
- Handles success or failure messages
- Updates the UI when done

## Requirement 3: Storing Data in a List

### The List Creation:

```python
formatted_new_interests = re.sub(r'\s*,\s*', ', ', new_interests.strip())
current_interests = user.interests.split(', ') if user.interests else []
combined_interests = list(set(current_interests + formatted_new_interests.split(', ')))
```

Here's how this part stores data in a list:
- It cleans up the format of the interests string
- It splits the user's current interests into a list
- It splits the new interests into another list
- It combines both lists and removes duplicates (using a set)
- It converts everything back to a clean list in `combined_interests`

## Requirement 4: Using Data from the List

### Using the List Data:

```javascript
function createInterestCards(interests) {
    const interestsSection = document.getElementById('interestsSection');
    interestsSection.innerHTML = '';
    
    if (!interests || interests.length === 0) {
        const placeholderInterests = ['Gaming', 'Reading', 'Music', 'Art'];
        placeholderInterests.forEach((interest, index) => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <h4>${interest}</h4>
                <img src="https://placehold.co/300x200/d34e3f/a3adbf/png?text=${interest}" alt="${interest}">
                <button onclick="deleteInterest('${interest}')">Delete</button>
                <button onclick="editInterest('${interest}')">Edit</button>
            `;
            interestsSection.appendChild(card);
        });
        return;
    }

    interests.forEach(interest => {
        const card = document.createElement('div');
        card.className = 'card';
        card.innerHTML = `
            <h4>${interest}</h4>
            <img src="https://placehold.co/300x200/d34e3f/a3adbf/png?text=${interest}" alt="${interest}">
            <button onclick="deleteInterest('${interest}')">Delete</button>
            <button onclick="editInterest('${interest}')">Edit</button>
        `;
        interestsSection.appendChild(card);
    });
}
```

This function takes our list of interests and:
- Goes through each interest one by one
- Creates a card on the screen for each one
- Shows the interest name and a placeholder image
- Adds buttons to edit or delete each interest
- Handles empty lists by showing default interests

## Summary

These four code segments complete the following:
1. Define a procedure to update interests
2. Call that procedure from the user interface
3. Store the interests in a list
4. Display those interests to the user