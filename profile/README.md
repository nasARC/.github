# Team nasARC | BioIndex

Try out [BioIndex](https://bioindex.nasarc.online)!

nasARC on [Nasa Space Apps](https://www.spaceappschallenge.org/2025/find-a-team/arc15/)

Our project aims to create a nexus for all space biology resources, through a quick, accurate and customizable search among a wide range of data, and integration with AI, providing answers at a moments notice. The search features benefit from the custom AI RAG pipeline, which itself was developed using agents with access, through toolchains, to the resources that we transformed and put in a vector database.

With the BioIndex website, you can quickly access search results from the 608 space biology publications, or talk to an AI that is knowledgable about all of them; and while viewing each article separately, ask a chatbot specific questions from the articles. 

## The Development of BioIndex

#### 1. Collecting and Formatting The Data
We began by downloading the study metadata from the provided CSV file using the Metapub Python library, which allows us to access the PubMed records of the NASA-led studies. The next step involved cleaning the dataset by handling missing values and correcting any discrepancies in the study information. We then standardized the fields, such as author names and publication dates, and filled in some missing fields using LLMs. 
#### 2. Embedding The Data
Once the publications had been downloaded and processed, we ran them through the our embedding pipeline. Our goal with embedding is to generate vectors from the article, which will be stored in the vector database to be queried by the search engine. We researched some advanced RAG techniques, and generated vectors from not only existing data such as publications' Titles, Abstracts and Content, but also synthetically generated Keywords and Questions directed at the publication.
#### 3. Creating A Search Algorithm
For our search algorithm, we began by embedding the user's search query. The embedding vector is used to rank documents in the vector database according to its similarity with the documents vector. The vectors are compared using cosine similarity. The ranked documents are then filtered according to the users request. The top k documents after filtering are passed as context onto the LLM to be used when answering the user's queries.
#### 4. Customizing The LLM
We used the Qdrant Client to enhance the agent’s responses by integrating relevant contextual information. The agent utilizes Retrieval-Augmented Generation (RAG) techniques, which combine external knowledge sources with the model’s outputs. By querying a vector database for context-specific data, the agent is able to provide more accurate, relevant, and detailed answers.  The agent performs these queries using a variety of tools we provide, including citation generation, deep research capabilities, and article querying. This allows the agent to tailor its responses based on the specific needs of the user’s query.
#### 5. Server Setup
We needed a server to perform various tasks, such as hosting our website, handling API traffic, and storing the vector database. After first setting up Docker, we created containers for Caddy (for url routing) and Qdrant. Although some issues arose such as the server provider going down in the middle of the competition, we managed to get a steady server.
#### 6. Project Structure
Below is the flowchart for BioIndex. It provides an overview of how data is processed and moves through our search engine system.

<img width="3636" height="2406" alt="bioindex_flowchart" src="https://github.com/user-attachments/assets/dd7904bb-167f-449c-89a2-d02c4761ce81" />

_Figure 1, BioIndex Flowchart_

#### 7. Making Data Accessible
In our website written with ReactJS, you will find all this data at your fingertips, with a design that focuses on user experience without compromising on style. Through the use of many libraries, detailed in our repository's readme, the access to the data has become fast, aesthetically pleasing, and most importantly, tailored for the end-user.
#### 8. Challenges We Faced
We encountered many challenges during the hackathon, one of which was the aforementioned crashing of our server provider, right when we were generating the embeddings for the publications. We lost more than 6 hours of computing time, which meant we were only able to embed a subset of the original 600 documents, despite the program being fully capable of it.

## Use of AI

AI was used very minimally in the development of this project.
ChatGPT was used minimally fot various purposes such as brain storming and research. We leveraged our student license to GitHub Copilot, using it mainly for code completion.

Obviously in accordance with the challenge, the project itself makes heavy use of AI, including two AI chatbots embedded with a huge amount of data, and an AI-powered search algorithm.

## Nasa Data Used

[Space Biology Publications](https://github.com/jgalazka/SB_publications/blob/main/SB_publication_PMC.csv)


## Other Links

- [React Frontend Repository](https://github.com/nasARC/BioIndexFE)
- [Publication Scraper Repository](https://github.com/nasARC/nasARC-scraper)
- [Python FastAPI Backend Repository](https://github.com/nasARC/BioIndex)
- [OpenAI Agents SDK](https://openai.github.io/openai-agents-python/)
- [Qdrant Client](https://qdrant.tech/documentation/)
