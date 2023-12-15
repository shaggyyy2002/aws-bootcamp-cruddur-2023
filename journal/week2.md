# Week 2 — Distributed Tracing

## What is Distributed Tracing?

Distributed tracing is a method of tracking application requests as they flow from frontend devices to backend services and databases. Developers can use distributed tracing to troubleshoot requests that exhibit high latency or errors.

## What is [HoneyComb](https://www.honeycomb.io/)?

Honeycomb is a fast analysis tool that helps you analyze your code’s performance and behavior to troubleshoot complex relationships within your system to solve problems faster. Honeycomb uses Opentelementry SDK which is then sent to Honeycomb.

![Opentelementry](../_docs/assets/Opentelementry.png)

Here's an example what we will se after everything's done and working.

![HoneyComb Example Trace](../_docs/assets/Honeycomb.png)

When creating a new dataset in Honeycomb it will provide all these installation insturctions
We'll add the following files to our `requirements.txt`

```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```

We'll install these dependencies:

```sh
pip install -r requirements.txt
```

Add to the `app.py`

```py
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```

```py
# Initialize tracing and an exporter that can send data to Honeycomb
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)
```

```py
# Initialize automatic instrumentation with Flask
app = Flask(__name__)
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```

Add teh following Env Vars to `backend-flask` in docker compose

```yml
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
OTEL_SERVICE_NAME: "${HONEYCOMB_SERVICE_NAME}"
```

You'll need to grab the API key from your honeycomb account:

```sh
export HONEYCOMB_API_KEY=""
gp env HONEYCOMB_API_KEY=""
```

## AWS XRay SDK

AWS X-Ray provides a complete view of requests as they travel through your application and filters visual data across payloads, functions, traces, services, APIs, and more with no-code and low-code motions.

### Setting Up AWS Xray

Make a `xray.json` file in `./aws/json/xray.json`
```json
{
  "SamplingRule": {
      "RuleName": "Cruddur",
      "ResourceARN": "*",
      "Priority": 9000,
      "FixedRate": 0.1,
      "ReservoirSize": 5,
      "ServiceName": "Cruddur",
      "ServiceType": "*",
      "Host": "*",
      "HTTPMethod": "*",
      "URLPath": "*",
      "Version": 1
  }
}

To apply the above things you will have to paste this command on your terminal
replace `FLASK_ADDRESS=SERVICE_NAME` ie. backend-flask

```sh
aws xray create-group \
   --group-name "Cruddur" \
   --filter-expression "service(\"$FLASK_ADDRESS\")"
```

If its setup properly you will get an output as 

```json
{
    "Group": {
        "GroupName": "Cruddur",
        "GroupARN": "arn:aws:xray:ap-south-1:746231924951:group/Cruddur/2LG66ET4D3DHULQQITKDUS4NA35TR54CXLSKVB6772UPSBNYYWPA",
        "FilterExpression": "service(\"backend-flask\")",
        "InsightsConfiguration": {
            "InsightsEnabled": false,
            "NotificationsEnabled": false
        }
    }
}
```

Create a Sampling Rule
```
aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json
```
The Output 

```json
{
    "SamplingRuleRecord": {
        "SamplingRule": {
            "RuleName": "Cruddur",
            "RuleARN": "arn:aws:xray:ca**-**-924951:sampling-rule/Cruddur",
            "ResourceARN": "*",
            "Priority": 9000,
            "FixedRate": 0.1,
            "ReservoirSize": 5,
            "ServiceName": "backend-flask",
            "ServiceType": "*",
            "Host": "*",
            "HTTPMethod": "*",
            "URLPath": "*",
            "Version": 1,
            "Attributes": {}
        },
        "CreatedAt": "2023-12-15T13:09:06+00:00",
        "ModifiedAt": "2023-12-15T13:09:06+00:00"
    }
}
```

### Middleware

Middleware speeds development of distributed applications by simplifying connectivity between applications, application components and back-end data sources.

![MiddleWare](../_docs/assets/middleware.png)










## **Resources:** 

- [HoneyComb](https://ui.honeycomb.io/)
- [HoneyComb Docs](https://docs.honeycomb.io/quickstart/)
- [Opentelementry](https://opentelemetry.io/docs/)
- [AWS XRay SDK](https://docs.aws.amazon.com/xray/latest/devguide/xray-sdk-python.html)
- [AWS Xray About](https://aws.amazon.com/xray/)
## **Tips/Best Practices**

- Everytime we change something important in the file commit the changes. 