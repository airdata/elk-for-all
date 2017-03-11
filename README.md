Make you shure the content of the 

 /opt/logstash/vendor/bundle/jruby/1.9/gems/logstash-output-elasticsearch-2.7.1-java/lib/logstash/outputs/elasticsearch/elasticsearch-template.json

is 

   {
      "template" : "logstash-*",
      "settings" : {
        "index.refresh_interval" : "5s"
      },
      "mappings" : {
        "_default_" : {
          "_all" : {"enabled" : true, "omit_norms" : true},
          "dynamic_templates" : [ {
            "message_field" : {
              "match" : "message",
              "match_mapping_type" : "string",
              "mapping" : {
                "type" : "string", "index" : "analyzed", "omit_norms" : true,
                "fielddata" : { "format" : "disabled" }
              }
            }
          }, {
            "string_fields" : {
              "match" : "*",
              "match_mapping_type" : "string",
              "mapping" : {
                "type" : "string", "index" : "analyzed", "omit_norms" : true,
                "fielddata" : { "format" : "disabled" },
                "fields" : {
                  "raw" : {"type": "string", "index" : "not_analyzed", "doc_values" : true, "ignore_above" : 256}
                }
              }
            }
          }, {
            "float_fields" : {
              "match" : "*",
              "match_mapping_type" : "float",
              "mapping" : { "type" : "float", "doc_values" : true }
            }
          }, {
            "double_fields" : {
              "match" : "*",
              "match_mapping_type" : "double",
              "mapping" : { "type" : "double", "doc_values" : true }
            }
          }, {
            "byte_fields" : {
              "match" : "*",
              "match_mapping_type" : "byte",
              "mapping" : { "type" : "byte", "doc_values" : true }
            }
          }, {
            "short_fields" : {
              "match" : "*",
              "match_mapping_type" : "short",
              "mapping" : { "type" : "short", "doc_values" : true }
            }
          }, {
            "integer_fields" : {
              "match" : "*",
              "match_mapping_type" : "integer",
              "mapping" : { "type" : "integer", "doc_values" : true }
            }
          }, {
            "long_fields" : {
              "match" : "*",
              "match_mapping_type" : "long",
              "mapping" : { "type" : "long", "doc_values" : true }
            }
          }, {
            "date_fields" : {
              "match" : "*",
              "match_mapping_type" : "date",
              "mapping" : { "type" : "date", "doc_values" : true }
            }
          }, {
            "geo_point_fields" : {
              "match" : "*",
              "match_mapping_type" : "geo_point",
              "mapping" : { "type" : "geo_point", "doc_values" : true }
            }
          } ],
          "properties" : {
            "@timestamp": { "type": "date", "doc_values" : true },
            "@version": { "type": "string", "index": "not_analyzed", "doc_values" : true },
            "source":{ "type": "string", "index": "not_analyzed"}
            "geoip"  : {
              "type" : "object",
              "dynamic": true,
              "properties" : {
                "ip": { "type": "ip", "doc_values" : true },
                "location" : { "type" : "geo_point", "doc_values" : true },
                "latitude" : { "type" : "float", "doc_values" : true },
                "longitude" : { "type" : "float", "doc_values" : true }
              }
            }
          }
        }
      }
    }
