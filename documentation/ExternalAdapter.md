# Chainlink External Adapter Workshop

[Original article](https://docs.google.com/document/d/e/2PACX-1vSlbBgXHatt1XOPthCHdJG2MlVP0Te9254kxLiCAE7R3yggzlwuVbPH5U8TSc1AjSCqy11ovhPPcQXL/pub)


### Dan Forbes ft. Jonny Huxtable

The purpose of this workshop is to showcase the power of Chainlink external adapters and their ability to extend the capabilities of the Chainlink node as well as explore their role in the Chainlink ecosystem. Participants will be guided through the process of creating a Chainlink external adapter and using it to request real-world data from a Chainlink node. This workshop will feature the LinkPool Bridges library, which makes writing Chainlink external adapters in the Go programming language easy. Jonny Huxtable, LinkPool co-founder & tech lead and member of the Chainlink core development team, will offer his offer insights on external adapter development, the LinkPool Bridges library and the marketplace for external adapters.

As part of this workshop, the external adapter will be deployed using AWS Lambda and Amazon API Gateway, which is a common way to expose external adapter capabilities. Although a credit card is required to sign up for an AWS account, following this workshop should not incur charges on a newly-created free-tier account. Please keep in mind that continued usage on your AWS account may result in charges. There are other methods for deploying external adapters, but they are out of the scope of this workshop.

Please note that in order to demonstrate external adapters in action, this workshop assumes that participants understand how to run a Chainlink node; issues related to this topic are out of the scope of this workshop.

This workshop will build on information from the [Chainlink + Remix Workshop](https://www.google.com/url?q=https://docs.google.com/document/d/e/2PACX-1vTfuGrmqJO_il0PzZY5iU5_HtmiEExu5t7XHzrj6rRVKZnOdvy3fUJzlIlTgd-FMrUl2A-9T9ndP7Nj/pub&sa=D&ust=1580319584150000).

The recording of this workshop can be found [here](https://www.google.com/url?q=https://t.co/ByIWBvNT8a?amp%3D1&sa=D&ust=1580319584150000).

### Environment

Since this workshop builds on the Chainlink + Remix Workshop mentioned above, it also makes the same assumptions with respect to the environment. Furthermore, I have the following applications installed, which are required for this workshop:

    [go](https://www.google.com/url?q=https://golang.org/&sa=D&ust=1580319584151000) v1.13
    [zip](https://www.google.com/url?q=https://linux.die.net/man/1/zip&sa=D&ust=1580319584152000) v3

### Code

The code used as a starting point for this workshop was found on github.com.
Steps

    Save the [code](https://www.google.com/url?q=https://github.com/linkpoolio/bridges/raw/master/examples/cryptocompare/main.go&sa=D&ust=1580319584153000) to a file called main.go.
    Use go to initialize a new module: go mod init cryptocompare-adapter
    Use go to fetch project dependencies: go get
    Use go to build the code: go build -o ./build/cryptocompare-adapter
    Use zip to create an archive of your code: zip -j cryptocompare-adapter.zip ./build/cryptocompare-adapter
    Use [AWS Lambda](https://www.google.com/url?q=https://aws.amazon.com/lambda/&sa=D&ust=1580319584154000) to create a new Function.

    Name: cryptocompare-adapter
    Runtime: Go 1.x

    Add code to your Function by uploading your zip archive.

    Code entry type: Upload a .zip file
    Runtime: Go 1.x
    Handler: cryptocompare-adapter

    Set the LAMBDA environment variable to true.
    Save the changes to your Function.
    Create a trigger for your Function.

    Trigger configuration: API Gateway
    API: Create a new API
    Security: Open

    Use the [API Gateway](https://www.google.com/url?q=https://aws.amazon.com/api-gateway/&sa=D&ust=1580319584157000) management console to remove Lambda Proxy Integration from your trigger.
    Deploy the changes to your trigger.
    Use the Chainlink node web UI to add a new Bridge to your Chainlink node.

    Name: cryptocompare
    Bridge URL: <API Gateway endpoint>

    Create a new Job that uses your Bridge:

{

  "initiators": [

    { "type": "web" }

  ],

  "tasks": [

    { "type": "cryptocompare" }

  ]

}

    Run the new Job.
    🚀🚀🚀
