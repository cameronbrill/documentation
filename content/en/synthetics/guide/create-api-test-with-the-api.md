---
title: Create an API test with the API
kind: guide
further_reading:
- link: "/api/latest/synthetics/"
  tag: "API"
  text: "Synthetics API"
- link: "/synthetics/"
  tag: "Documentation"
  text: "Manage your checks"
---

## Overview

This guide contains examples of configuration files you can use to create API tests.

To create API tests with the API, see the [JSON configuration examples](#json-configuration). To create a HTTP test with the Python client, see the [Python client example](#python-client).

For more information, see [Create an API test][1] in the API documentation.

## JSON configuration

### HTTP test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:production"
    ],
    "locations": [
        "azure:eastus",
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "http",
    "config": {
        "request": {
            "url": "https://example.com",
            "method": "GET"
        },
        "assertions": [
            {
                "operator": "lessThan",
                "type": "responseTime",
                "target": 1000
            },
            {
                "operator": "is",
                "type": "statusCode",
                "target": 200
            },
            {
                "operator": "is",
                "property": "content-type",
                "type": "header",
                "target": "text/html; charset=UTF-8"
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

### SSL test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:production"
    ],
    "locations": [
        "azure:eastus",
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "ssl",
    "config": {
        "request": {
            "host": "example.com",
            "port": 443
        },
        "assertions": [
            {
                "operator": "isInMoreThan",
                "type": "certificate",
                "target": 10
            },
            {
                "operator": "moreThanOrEqual",
                "type": "tlsVersion",
                "target": "1.3"
            },
            {
                "operator": "lessThan",
                "type": "responseTime",
                "target": 1000
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

### DNS test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:production"
    ],
    "locations": [
        "azure:eastus",
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "dns",
    "config": {
        "request": {
            "host": "example.com"
        },
        "assertions": [
            {
                "operator": "lessThan",
                "type": "responseTime",
                "target": 1000
            },
            {
                "operator": "is",
                "property": "A",
                "type": "recordSome",
                "target": "93.184.216.34"
            },
            {
                "operator": "is",
                "property": "NS",
                "type": "recordSome",
                "target": "a.iana-servers.net"
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

### TCP test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:production"
    ],
    "locations": [
        "azure:eastus",
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "tcp",
    "config": {
        "request": {
            "host": "example.com",
            "port": 443
        },
        "assertions": [
            {
                "operator": "lessThan",
                "type": "responseTime",
                "target": 1000
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

### UDP test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:prod"
    ],
    "locations": [
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "udp",
    "config": {
        "request": {
            "host": "example.com",
            "message": "UDP message",
            "port": 31337
        },
        "assertions": [
            {
                "operator": "lessThan",
                "type": "responseTime",
                "target": 1000
            },
            {
                "operator": "is",
                "type": "receivedMessage",
                "target": "UDP message response"
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

### ICMP test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:production"
    ],
    "locations": [
        "aws:us-west-2",
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "icmp",
    "config": {
        "request": {
            "numberOfPackets": 4,
            "host": "example.com"
        },
        "assertions": [
            {
                "operator": "lessThan",
                "property": "avg",
                "type": "latency",
                "target": 1000
            },
            {
                "operator": "is",
                "type": "packetLossPercentage",
                "target": 0
            },
            {
                "operator": "moreThanOrEqual",
                "type": "packetsReceived",
                "target": 1
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

### WebSocket test

{{< code-block lang="json" disable_copy="false" collapsible="true" >}}
{
    "status": "live",
    "tags": [
        "env:prod"
    ],
    "locations": [
        "aws:eu-west-3"
    ],
    "message": "<NOTIFICATION MESSAGE>",
    "name": "<TEST NAME>",
    "type": "api",
    "subtype": "websocket",
    "config": {
        "request": {
            "url": "ws://example.com:8081",
            "message": "websocket message"
        },
        "assertions": [
            {
                "operator": "lessThan",
                "type": "responseTime",
                "target": 1000
            },
            {
                "operator": "is",
                "type": "receivedMessage",
                "target": "connected!"
            }
        ]
    },
    "options": {
        "monitor_options": {
            "notify_audit": false,
            "locked": false,
            "include_tags": true,
            "new_host_delay": 300,
            "notify_no_data": false,
            "renotify_interval": 0
        },
        "tick_every": 60,
        "min_failure_duration": 0,
        "min_location_failed": 1
    }
}
{{< /code-block >}}

## Python client

### HTTP test

{{< code-block lang="python" disable_copy="false" collapsible="true" >}}
import os
from dateutil.parser import parse as dateutil_parser
from datadog_api_client.v1 import ApiClient, ApiException, Configuration
from datadog_api_client.v1.api import synthetics_api
from datadog_api_client.v1.models import *
from pprint import pprint

// See configuration.py for a list of all supported configuration parameters
configuration = Configuration(
    host = "https://api.datadoghq.com",
    api_key= {"apiKeyAuth": "<YOUR_API_KEY>","appKeyAuth": "<YOUR_APPLICATION_KEY>"}
)

// Enter a context with an instance of the API client
with ApiClient(configuration) as api_client:
    // Create an instance of the API class
    api_instance = synthetics_api.SyntheticsApi(api_client)
    body = SyntheticsAPITest(
        config=SyntheticsAPITestConfig(
            assertions=[
                SyntheticsAssertion(
                    operator="lessThan",
                    type="responseTime",
                    target=1000
                ),
            ],
            request=SyntheticsTestRequest(
                body="body_example",
                headers=SyntheticsTestHeaders(
                    **{"User-Agent": "value"}),
                method=HTTPMethod("GET"),
                no_saving_response_body=True,
                query={},
                timeout=60.0,
                url="https://httpbin.org/get",
            ),
        ),
        locations=[
            "aws:eu-west-2",
        ],
        message="message_example",
        name="name_example",
        options=SyntheticsTestOptions(
            follow_redirects=True,
            min_failure_duration=1,
            min_location_failed=1,
            #monitor_name="monitor_name_example",
            monitor_options=SyntheticsTestOptionsMonitorOptions(
                renotify_interval=0,
            ),
            monitor_priority=1,
            tick_every=30
        ),
        status=SyntheticsTestPauseStatus("live"),
        subtype=SyntheticsTestDetailsSubType("http"),
        tags=[
            "python-client",
        ],
        type=SyntheticsAPITestType("api"),
    )  # SyntheticsAPITest | Details of the test to create.

    // example passing only required values which don't have defaults set
    try:
        // Create an API test
        api_response = api_instance.create_synthetics_api_test(body)
        pprint(api_response)
    except ApiException as e:
        print("Exception when calling SyntheticsApi->create_synthetics_api_test: %s\n" % e)
{{< /code-block >}}

## Further Reading

{{< partial name="whats-next/whats-next.html" >}}

[1]: /api/latest/synthetics/#create-an-api-test
