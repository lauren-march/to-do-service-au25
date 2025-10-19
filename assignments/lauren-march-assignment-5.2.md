# Assignment 5.2 - Open API Specification document

## Manually created OAS document

```yaml

openapi: 3.1.0
info:
 title: The dog database
 version: 0.0.1
 contact:
    name: Lauren March

servers:
 - url: http://localhost:3000
   description: Local server for testing

tags:
  - name: dogs
    description: "Dog related endpoints that manage dog entries." 

paths:
 /dogs:
   get:
    summary: Get all dogs
    description: "Returns a list of all dogs in the system.
      There are certain required properties each entry must have."
    tags:
      - dogs
    operationId: getAllDogs
    responses:
      '200':
        description: A list of dogs
        content:
          application/json:
            schema:
              type: object
              properties:
                dogs:
                  type: array
                  items:
                    type: object
                    properties: 
                      id:
                        description: ID of dog object
                        type: integer
                        examples: [1]                      
                      breed:
                        description: Type of dog breed
                        type: string       
                        examples: [border collie]                 
                      color:
                        description: Color of dog
                        type: string
                        enum: [black, white, brown, mixed, red, gold, brindle]
                        examples: [black]
                      weight: 
                        description: Weight of dog in pounds (lbs)
                        type: number 
                        examples: [55.3]
                      temperament: 
                        description: Temperament of dog. 
                        type: array
                        examples: [high energy]
                    required: 
                      - id
                      - breed
                      - weight
                      - temperament
                      
      '404':
        description: "Lost dog not found"
        content:
          application/json:
            schema:
              type: object
              properties:
                  message:
                    type: string
                    examples: [Lost dog not found, contact nearest animal shelter]

```

## AI-generated OAS document

If you used an AI tool to create a version of your specification:

I had ChatGPT help when I had errors and to give me suggestions for additional property options (like example:, and enums). Once I had it help me walk though how to format the YAML properly, I asked it to for get everything that we talked about so far. In theory (not entirely convinced since it was pretty close to what I already had and snippets of what I had shown see: Shaggy Dog, and my name) this gave me a clean slate to ask the full AI prompt below.

I did get some hallucinations or just outdated information. For example, I asked for additional property options and it gave me 'example', but Swagger underlined this in yellow and stated it was deprecated. 

### AI prompt

```text

I want you to create a YAML OAS file. I want it to be a localhost dog database. I want you to include only a single resource with the get method. The Get method should have the required summary and operationId information. I also want a dog tag. I want the single resource to have an id, breed, color, and weight property with at least a description and a type (please feel free to add more as you see fit). There should be a single 200 success response content that contains a application/json object that contains an array of objects. I also want a 404 response with a string. If you choose to add more property elements, please note that example is deprecated and examples is the replacement that requires an array.

```

### AI-generated document

```yaml

openapi: 3.1.0
info:
  title: The Dog Database
  version: 1.0.0
  contact:
    name: Lauren March
servers:
  - url: http://localhost:3000

tags:
  - name: Dogs
    description: All dog-related endpoints for retrieving dog data.

paths:
  /dogs:
    get:
      summary: Get all dogs
      description: Returns a list of all dogs in the system.
      operationId: getAllDogs
      tags:
        - Dogs
      responses:
        '200':
          description: A list of dogs
          content:
            application/json:
              schema:
                type: object
                properties:
                  dogs:
                    type: array
                    items:
                      type: object
                      properties:
                        id:
                          description: Unique identifier for the dog
                          type: string
                          examples: ["1", "2", "3"]
                        breed:
                          description: The dog's breed
                          type: string
                          maxLength: 50
                          examples: ["Shaggy Dog", "Golden Retriever", "Bulldog"]
                        color:
                          description: The dog's primary color
                          type: string
                          enum: [white, black, brown, golden, mixed]
                          examples: ["white"]
                        weight:
                          description: The dog's weight in pounds
                          type: number
                          format: float
                          minimum: 0
                          examples: [44.0]
        '404':
          description: Lost dog not found
          content:
            application/json:
              schema:
                type: string
                examples: ["Dog not found in the database."]


```