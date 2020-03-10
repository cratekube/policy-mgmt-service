# Design Requirements

## Policy Declaration Format
![Generic badge](https://img.shields.io/badge/BUSINESS-MVP-GREEN.svg) 
As a user, I want the default policy to be stored as YAML, so that policy details can be easily retrieved, because otherwise there will not be a standard way for services to interpret policies. 

## Sane Default
![Generic badge](https://img.shields.io/badge/BUSINESS-MVP-GREEN.svg) 
As a user, I want a default policy to be set at runtime, so that the policy-mgmt-service provides a sane default, because it is easier to prove compliance measures from a single location. 

## Static Content
![Generic badge](https://img.shields.io/badge/TECHNICAL-MVP-GREEN.svg) 
As a user, I want the default policy to be served as static content, so that I can fetch the policy, because a full api is not necessary for MVP.

## Policy Change Events 
![Generic badge](https://img.shields.io/badge/TECHNICAL-POSTMVP-YELLOW.svg)

## Contract Documentation
![Generic badge](https://img.shields.io/badge/BUSINESS-MVP-GREEN.svg) 
As a user, I want a contract documentation for policies, so that consumers know how to interpret policies, otherwise users will receive a YAML that they don't know what to do with. 

## Policy Coupling
![Generic badge](https://img.shields.io/badge/BUSINESS-MVP-GREEN.svg) 
As a user, I want policies to be loosely coupled to services within CrateKube, so that the Policy Management Service does not need to be aware of service specific requirements, because complexity increases greatly with each additional service. 

## Policy Requirement Levels
![Generic badge](https://img.shields.io/badge/TECHNICAL-MVP-GREEN.svg) 
As a user, I want detailed policy requirement levels based on [RFC2119](https://www.ietf.org/rfc/rfc2119.txt), so that I know whether a requirement is mandatory, because I may need to abort processing if I can't satisfy the requirement. 

## Security
![Generic badge](https://img.shields.io/badge/BUSINESS-MVP-GREEN.svg) 
As a user, I want token authentication and authorization implemented at runtime, so that REST resources are protected, because without security cloud resources may be manipulated by unauthorized users. 

# Decisions Made During Requirements Gathering
The following decisions were made during requirements gathering:

## YAML vs DB
For MVP a decision was made to use YAML for storing policies rather than a database. The reason for this implementation is that no manipulation of policies is initially required and export of policies is easily performed. 

## RFC2119
Policy requirement levels should be based off a standard specification so that clients are able to implement logic for handling mandatory requirements and optional requirements. Each verb, such as `must`, `should`, or `may`, is expected to be clearly detailed so that clients can choose the best course of action for policy implementation. 

## REST vs Static Content
MVP does not require any manipulation of policy requirements and as such does not need a full REST API for working with policies. The quickest route to MVP allows the policy yaml to be served as static content. 
