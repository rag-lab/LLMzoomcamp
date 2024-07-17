# LLMzoomcamp Module 1


http://127.0.0.1:9200/

run elastic search
docker run -it \
    --rm \
    --name elasticsearch \
    -p 9200:9200 \
    -p 9300:9300 \
    -m 4GB \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    docker.elastic.co/elasticsearch/elasticsearch:8.14.3

#from localhost
docker run -it \
    --rm \
    --name elasticsearch \
    --net elastic \
    -p 9200:9200 \
    -p 9300:9300 \
    -m 4GB \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    docker.elastic.co/elasticsearch/elasticsearch:8.14.3


export ELASTIC_PASSWORD="bbvapMWzvbcykMLn1GkR"


#generate password
docker exec -it elasticsearch ./bin/elasticsearch-setup-passwords auto

PASSWORD elastic = eKWQYCwOLpREZmHZ0LnR

Changed password for user apm_system
PASSWORD apm_system = lmxjgEN1Qg6AThULnOmJ

Changed password for user kibana_system
PASSWORD kibana_system = biMIvm1ATirONpBBK4PP

Changed password for user kibana
PASSWORD kibana = biMIvm1ATirONpBBK4PP

Changed password for user logstash_system
PASSWORD logstash_system = LhVFVBS6f0PgfiEJvhCJ

Changed password for user beats_system
PASSWORD beats_system = BNUaqIcKsgdoDPUrl9O0

Changed password for user remote_monitoring_user
PASSWORD remote_monitoring_user = jA9VxU70BkrYZpN1qaF8

Changed password for user elastic
PASSWORD elastic = eKWQYCwOLpREZmHZ0LnR

direct from the hub
docker run -it \
    --rm \
    --name elasticsearch \
    -p 9200:9200 \
    -p 9300:9300 \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    elasticsearch:8.4.3


index settings
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    },
    "mappings": {
        "properties": {
            "text": {"type": "text"},
            "section": {"type": "text"},
            "question": {"type": "text"},
            "course": {"type": "keyword"} 
        }
    }
}


query
{
    "size": 5,
    "query": {
        "bool": {
            "must": {
                "multi_match": {
                    "query": query,
                    "fields": ["question^3", "text", "section"],
                    "type": "best_fields"
                }
            },
            "filter": {
                "term": {
                    "course": "data-engineering-zoomcamp"
                }
            }
        }
    }
}


We use "type": "best_fields". You can read more about different types of multi_match search in elastic-search.md.

When we use the OpenAI Platform, we're charged by the number of tokens we send in our prompt and receive in the response.

The OpenAI python package uses tiktoken for tokenization:

sudo pip3 install tiktoken
