# Setup docker postgres instance
Load and run the postgres docker Database
`docker run --name itmc_project_db -p 127.0.0.1:5432:5432 -e POSTGRES_PASSWORD=pw postgres`

## Loading db schema into docker
Copy the sql script into the docker container
`docker cp schema.sql itmc_project_db:/`

## Run the sql schema file to build the db
`docker exec -it itmc_project_db psql -U postgres -d postgres -f /schema.sql`

# Building a chatbot
- type in your start urls  into the `seed_urls` variable and save.
- run `python chatbot_knowledge_discovery.py`

After completion all chatbot texts should be saved in the database and `n` clusters are created (`n` can be set in the clusterer.py module).
Each cluster contains 5 texts with their respective match percentge to the center of that cluster.

# searching the existing chatbot
- type in a question into `search.py` and save.
- run `python search.py`

The question is then encoded and compared to the existing texts in the database. A list of the 5 closest semantic texts is then returned.