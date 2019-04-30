# Ubuntu Development Environment Setup on Windows 10

## Install updates

```sudo apt-get update```

## Install Git
```sudo apt-get install git-core```

```git --version```

## Install Node.js
```sudo apt-get install curl python-software-properties```

```curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -```

```sudo apt-get update```

```sudo apt-get install nodejs```

```node -v```

```npm -v```

### Building Serverless API
```sudo npm install -g serverless```

```serverless create --template aws-nodejs --path helloworld-service```

```cd helloworld-service```

```Configure IAM user``` in AWS Console with username ```serverless-agent``` with ```Programmatic access``` and providing ```Administrative Access```

```
export AWS_ACCESS_KEY_ID=AKIASUT4R3QTU4XXXXXX
export AWS_SECRET_ACCESS_KEY=s8PWQJAkBeXXXXXX/X/zpWk/Fo02XXXXXXX
```

```serverless deploy -v```

```serverless invoke -f hello -l```

```serverless logs -f hello -t```
