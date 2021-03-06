[![Build Status](https://travis-ci.com/pulumi/pulumi-awsx.svg?token=eHg7Zp5zdDDJfTjY8ejq&branch=master)](https://travis-ci.com/pulumi/pulumi-awsx)

# Pulumi AWS Infrastructure Components

Pulumi's framework for Amazon Web Services (AWS) infrastructure.

This package is meant for use with the Pulumi CLI.  Please visit [pulumi.io](https://pulumi.io) for
installation instructions.

The AWS Infrastructure package is intended to provide [component](https://pulumi.io/reference/programming-model.html#components) wrappers around many core AWS 'raw' resources to make them easier and more convenient to use.  In general, the `@pulumi/awsx` package mirrors the module structure of `@pulumi/aws` (i.e. `@pulumi/awsx/ecs` or `@pulumi/awsx/ec2`).  These [components](https://pulumi.io/reference/programming-model.html#components) are designed to take care of much of the redundancy and boilerplate necessary when using the raw AWS resources, while still striving to expose all underlying functionality if needed.

The AWS Infrastructure package undergoes constant improvements and additions.  While we will strive to maintain backward compatability here, we will occasionally make breaks here as appropriate if it helps improve the overall quality of this package.

The AWS Infrastructure package exposes many high level abstractions.  Including, but not limited to:

* [`apigateway`](https://github.com/pulumi/pulumi-awsx/blob/master/nodejs/awsx/apigateway). A module that makes creating API Gateway RestApis easily.  It includes native support to easily route incoming requests to AWS Lambdas, S3 buckets, or proxying requests to internal Load Balancer endpoints.

* [`autoscaling`](https://github.com/pulumi/pulumi-awsx/blob/master/nodejs/awsx/autoscaling). A module that makes creating auto-scaling launch configurations and launch groups easier.   Note: given an awsx `ecs.Cluster`, the easiest way to create an auto-scaling group is to just call [`createAutoScalingGroup`](https://github.com/pulumi/pulumi-awsx/blob/0b432e320c6929866038507e997d55c8d8f62bc3/nodejs/awsx/ecs/cluster.ts#L78) on it.  This will produce an auto-scaling group already property configured for that cluster.

* [`ec2`](https://github.com/pulumi/pulumi-awsx/blob/master/nodejs/awsx/ec2).  A module that makes it easier to work with your AWS network, subnets, and security groups.  By default, the resources in the package follow the [AWS Best Practices](
  https://aws.amazon.com/answers/networking/aws-single-vpc-design/), but can be configured as desired in whatever ways you want.  Most commonly, this package is used to acquire the default Vpc for a region (using [`Vpc.getDefault`](https://github.com/pulumi/pulumi-awsx/blob/0b432e320c6929866038507e997d55c8d8f62bc3/nodejs/awsx/ec2/vpc.ts#L118).  However, it can also be used to easily create or augment an existing Vpc.

* [`ecs`](https://github.com/pulumi/pulumi-awsx/blob/master/nodejs/awsx/ecs).  A module that makes it easy to create and configure clusters, tasks and services for running containers. Convenience resources are created to make the common tasks of creating EC2 or Fargate services and tasks much simpler.

* [`lb`](https://github.com/pulumi/pulumi-awsx/tree/master/nodejs/awsx/lb).  A module for simply setting up [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/). This module provides convenient ways to set up either `Network` or `Application` load balancers, along with the appropriate ELB Target Groups and Listeners in order to have a high availability, automatically-scaled service.  These ELB components also work well with the other awsx components.  For example, an [`lb.TargetGroup`](https://github.com/pulumi/pulumi-awsx/blob/f60ea6dec5c2450bf0bb457981a3091c094e9631/nodejs/awsx/lb/targetGroup.ts#L24) can be passed in directly as the `portMapping` target of an [`ecs.Container`](https://github.com/pulumi/pulumi-awsx/blob/0b432e320c6929866038507e997d55c8d8f62bc3/nodejs/awsx/ecs/container.ts#L185).

* ~~`Network`~~. Deprecated.  Use [ec2.VPC](https://github.com/pulumi/pulumi-awsx/blob/0b432e320c6929866038507e997d55c8d8f62bc3/nodejs/awsx/ec2/vpc.ts#L25) instead.

* ~~`Cluster`~~. Deprecated.  Use [ecs.Cluster](https://github.com/pulumi/pulumi-awsx/blob/0b432e320c6929866038507e997d55c8d8f62bc3/nodejs/awsx/ecs/cluster.ts#L26) instead.


## Installing

This package is available in JavaScript/TypeScript for use with Node.js.  Install it using either `npm`:

    $ npm install @pulumi/awsx

or `yarn`:

    $ yarn add @pulumi/awsx

## Reference

For detailed reference documentation, please visit [the API docs](
https://pulumi.io/reference/pkg/nodejs/@pulumi/awsx/index.html).
