# Knight Path Technical Take Home

Congrats on making it to our technical evaluation!  To help us understand your capabilities with our back-end technologies, we've put together a small project.

Your task is to create 3 serverless compute functions (azure function, AWS lambda, or anything else you prefer) that will help solve a small chess problem asynchronously.

If you don't play chess no worries you only need to know how a knight moves (https://en.wikipedia.org/wiki/Knight_(chess))


The user flow as follows:
1. User calls the first API with the start and end postion of the knight and gets back a tracking Id.
2. User calls the second API with the tracking id and receives a response showing the shortest path for the knight as well as the number of moves.

Here is a demo (using postman to call deployed solution) to make it more clear (https://dev.azure.com/Venteur/Venteur/_git/interview-screening-knightpath-starter?path=/TakeHome-KnightPath.postman_collection.json).

You are expected to build and deploy working functions.  This work has been designed to be no more than a couple of hours from start to finish. Below are various details that you may find helpful in completing the project.

## Requirements

1. You should use 3 separate serverless compute (One to create the request, one to process the request and one to return the results).
2. After receiving the positions in a first function you should trigger the second function to calculate the moves asynchronously.
3. You should handle and display the errors appropriately.
4. You should use a storage to keep the data you have calculated.
5. Think about ways you can leverage the stored data to optimize your solution.


## API Details

API 1 endpoint:

POST https://[...]/knightpath

query params:

```tsx
	source: string;
	target: string;
```

response body schema:

```tsx
	string or any object containing the operation Id;
```

sample request:

```tsx
    https://knightpath.azurewebsites.net/api/knightpath?source=C1&target=F7
```

sample response:

```tsx
    "Operation Id 941ecdd6-44fd-415c-ae7a-619cffc346e7 was created. Please query it to find your results."
```

API 2 endpoint:

GET https://[...]/knightpath

query params:

```tsx
	operationId: string;
```

response body schema:

```tsx
type KnightPathResponse = {
    shortestPath: string; (or string[])
    numberOfMoves: int;
    starting: string;
    ending: string;
    operationId: string;
}
```

sample request:

```tsx
    https://knightpath.azurewebsites.net/api/knightpath?operationId=941ecdd6-44fd-415c-ae7a-619cffc346e7
```

sample response:

```tsx
{
    "starting": "A1",
    "ending": "D5",
    "shortestPath": "A1:C2:E3:D5",
    "numberOfMoves": 3,
    "operationId": "941ecdd6-44fd-415c-ae7a-619cffc346e7"
}
```

## Submission

Email dev@venteur.co with the following:
1. Github repo link of the project
2. Link to the hosted serverless compute application
3. Explain in a few paragraphs your key design choices and implementation and any notes you deem relevant while for us toreview your project.