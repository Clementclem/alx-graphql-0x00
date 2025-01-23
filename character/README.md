 Write a Query to Get a Specific Character by ID
mandatory
Objective: Learners will write a GraphQL query to retrieve a specific character’s information using their ID.

Use the following Endpoint

Instructions:

Write a GraphQL query using the character(id: ID!) field to fetch the details of a character. Use ids 1, 2, 3, 4
Include the following fields in your query: id, name, status, species, type, gender



# Character Query by ID

## Objective
Write GraphQL queries to fetch details of specific characters using their ID from the given API.

## Endpoints
- GraphQL API Endpoint: [Insert API URL here]

## Queries
For each ID (1, 2, 3, 4), the following fields were retrieved:
- `id`
- `name`
- `status`
- `species`
- `type`
- `gender`

## File Structure
- **character-id-1.graphql**: Query to fetch character with ID 1.
- **character-id-1-output.json**: JSON response for character ID 1.
- **character-id-2.graphql**: Query to fetch character with ID 2.
- **character-id-2-output.json**: JSON response for character ID 2.
- **character-id-3.graphql**: Query to fetch character with ID 3.
- **character-id-3-output.json**: JSON response for character ID 3.
- **character-id-4.graphql**: Query to fetch character with ID 4.
- **character-id-4-output.json**: JSON response for character ID 4.

## Usage
1. Run each `.graphql` query in a GraphQL client or through a script.
2. Verify the output and save it in the respective `.json` file.

