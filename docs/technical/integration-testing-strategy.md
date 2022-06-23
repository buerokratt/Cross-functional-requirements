# Integration Testing Strategy

This document outlines the integration testing strategy for all Bürokratt components.

## What is Integration Testing?

Integration tests are tests that ensure that one or more components of a system work correctly in their integrated form. For the purposes of Bürokratt, "integrated form" can be understood to be when they are deployed to Azure and configured correctly.

Integration tests assure that components integrate with each other as expected and test "paths" through the overall system via integrated components.

Integration tests can test very short, specific paths or much broader end-to-end paths.

Integration tests can test both expected outcomes and also test for edge scenarios such as error cases.

In the wider technical community, this kind of testing can also be known as "System Testing". The term "System Testing" generally leans towards testing only the whole system, not sub-components within it. System testing can also be called "end to end" testing.

The term "smoke testing" can also be used which is generally referred to as a type of system test which just asserts that the expected path through the system works correctly.

For the purposes of Bürokratt and this strategy, all of the above terms can be collectively understood as "integration tests".

Integration tests are not to be confused with "unit tests" which make assertions of specific code modules and therefore operate at the code level, before the system component has been deployed and integrated. By the time a component is exposed to integration tests, it should have already passed all of its unit tests.

## Tests and Assertions

This section will outline the integration tests that will be created and what assertions they will make

### Classify a message: normal path

This test asserts that when DMR receives an unclassified message which is correctly formed, it is able to classify it and reply to the calling participant with the classification. This is steps 1-4 from [Milestones.md](https://github.com/buerokratt/Project-Documentation-Management/blob/main/Milestones.md) and represents milestone 1.

Input: Test generates a correctly formed, unclassified message with all appropriate headers and submits it to DMR.

Expected output: DMR calls back to the participant defined by the `X-Sent-By` header with a classification. Assert that the classification is what was expected for the message contents.

### Bot-to-bot: normal path

This test asserts that a bot can route a classified message to another bot via DMR. This represents steps 6 and 7 from [Milestones.md](https://github.com/buerokratt/Project-Documentation-Management/blob/main/Milestones.md) and milestone 2

Input: Test generates a correctly formed, classified message with all appropriate headers and submits it to DMR.

Expected output: DMR forwards the message to the correct participant. Test asserts that the message was received and is in the expected format.

## How to make assertions on HTTP calls

The architecture of the Bürokratt system operates on a series of chained HTTP requests and the final step of any interaction is for a participant (represented as a mock bot currently) to receive a HTTP request from DMR.

In order to assert that these HTTP requests are being received we ???

1. Test-specific endpoint that returns inbound http requests received by component in x time period (a bit like https://github.com/martinkearn/Table-Log-Api)
2. Logs (app insights logs)



## Platform and Tooling

## Pipelines

