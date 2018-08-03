# Introduction

Welcome to the edChain API! You can use our API to access edChain API endpoints, which can get information on various courses in our database.

We have language bindings JavaScript and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

Using a decentralized network and blockchain technology, edChain enables students, educators, and employers to interact directly and participate in the exchange of education and learning without the involvement of intermediaries.

## Documentation

To contribute to the documentation please follow instructions below.

Please install Ruby. You will also need to install Git. Follow instructions [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to install it. Once complete, please get edchain running on your machine. The instructions are stated below.

$gem install bundler

$gem install nokogiri -v 1.6.2.1 -- --use-system-libraries

$bundle install

$bash deploy.sh

All changes need to be done at inludes folder. slate/source/includes/
After making changes to .md file at slate/source/includes/ run deploy.sh to see the updated changes.
