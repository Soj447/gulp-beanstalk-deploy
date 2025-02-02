gulp-beanstalk-deploy
=====
[![Build Status](https://travis-ci.org/a0ly/gulp-beanstalk-deploy.svg?branch=master)](https://travis-ci.org/a0ly/gulp-beanstalk-deploy)
[![npm version](https://badge.fury.io/js/gulp-beanstalk-deploy.svg)](https://badge.fury.io/js/gulp-beanstalk-deploy)
[![Downloads](https://img.shields.io/npm/dt/gulp-beanstalk-deploy.svg)](https://www.npmjs.com/package/gulp-beanstalk-deploy)
[![Dependency Status](https://david-dm.org/a0ly/gulp-beanstalk-deploy.svg)](https://david-dm.org/a0ly/gulp-beanstalk-deploy)

> A gulp plugin for deployment your application to AWS Elastic Beanstalk

This plugin helps you to integrate your deployment task on the Amazon AWS Elasticbeanstalk service into gulp. Your deployment job will be more mainatainable and efficient, so that you can increase productivity.

## Getting Started

You can install plugin by this command:
```shell
npm install gulp-beanstalk-deploy
```

## Overview
```javascript
gulp.task('deploy', function(cb) {
  eb({
    // options here
  }, cb)
});
```

### Options

A * indicates a mandatory option.

##### accessKeyId

* Type: `string`
* Default: `~/.aws/credentials`

The aws access key id. If nothing passwed, it will use your local aws profile credential.

##### secretAccessKey

* Type: `string`
* Default: `~/.aws/credentials`

The aws access secret access key. If nothing passwed, it will use your local aws profile credential.

##### region *
* Type: `string`

Your application region. It must be provided.

##### applicationName *
* Type: `string`

Your application name. It must be provided.

##### environmentName *
* Type: `string`

Your application enviroment name. It must be provided.

##### versionLabel
* Type: `string`
* Default: sourceBundle file name without the extension

##### description
* Type: `string`

Your deployment description.

##### settings
* Type: `Array`

Your environment setting parameters.

##### waitForDeploy
* Type: `boolean`
* Default: true

##### checkIntervalSec
* Type: `number`
* Default: 2sec

Interval time to check deploying status. (sec)

##### s3Bucket
* Type: `object`
* Default:
```javascript
{
    bucket: // applicationName
    key: // sourceBundle basename
}
```

##### sourceBundle *
* Type: `string`

archive file path to upload. It must exists in your local file system, which means the archive file must be prepared before deployment task.

##### serverSideEncryption
* Type: `string`

If the object is stored using server-side encryption either with an AWS KMS customer master key (CMK) or an Amazon S3-managed encryption key, the response includes this header with the value of the server-side encryption algorithm used when storing this object in Amazon S3 (for example, AES256, aws:kms)

##### tagsToAdd
* Type: `dict`
* Default:
```javascript
[]
```
* format:
```javasctipt
{'key': 'value' ...}
```

Tag to set.

##### tagsToRemove
* Type: `dict`
* Default:
```javascript
[]
```
* format:
```javasctipt
{'key': 'value' ...}
```

Tag to remove.

## Usage Example
``` javascript
var gulp = require('gulp');
var eb = require('gulp-beanstalk-deploy');

gulp.task('deploy', function(cb) {
  eb({
    accessKeyId: 'Your AWS accessKeyId', // optional
    secretAccessKey: 'Your AWS secretAccessKey', // optional
    region: 'us-west-1', // required
    applicationName:'gulp-beanstalk-deploy',
    environmentName: 'gulp-beanstalk-deploy-env',
    versionLabel: '1.0.0',
    sourceBundle: './archive.zip',
    description: 'description here',
    serverSideEncryption: 'AES256',
    account_id: 'Your AWS accountId',
    tagsToAdd: {'key': 'value' ...},
    tagsToRemove: {'Key': 'value' ...}
  }, cb);
});
```

## License
MIT
