# Bucket Stream

**Find interesting Amazon S3 Buckets by watching certificate transparency logs.**

This tool simply listens to various certificate transparency logs (via certstream) and attempts to find public S3 buckets from permutations of the certificates domain name.

![Demo](https://i.imgur.com/B0kesTo.png)

**Be responsible**. I mainly created this tool to highlight the risks associated with public S3 buckets and to put a different spin on the usual dictionary based attacks. Some quick tips if you use S3 buckets:

1) Randomise your bucket names! There is no need to use `company-backup.s3.amazonaws.com`.
2) Set appropriate permissions and audit regularly. If possible create two buckets - one for your public assets and another for private data.
3) Be mindful about **your data**. What are suppliers, contractors and third parties doing with it? Where and how is it stored? These basic questions should be addressed in every info sec policy.
4) Try [Amazon Macie](https://aws.amazon.com/macie/) - it will automatically classify and secure sensitive data.

Thanks to my good friend David (@riskobscurity) for the idea.

## Installation

Python 3.4+ and pip3 are required. Then just:

1. `git clone https://github.com/eth0izzle/bucket-stream.git`
2. *(optional)* Create a virtualenv with `pip3 install virtualenv && virtualenv .virtualenv && source .virtualenv/bin/activate`
2. `pip3 install -r requirements.txt`
3. `python3 bucket-stream.py`

## Usage

Simply run `python3 bucket-stream.py`.

If you provide AWS access and secret keys in `config.yaml` Bucket Stream will attempt to access authenticated buckets and identity the buckets owner.

    usage: python3 bucket-stream.py

    Find interesting Amazon S3 Buckets by watching certificate transparency logs.

    optional arguments:
      -h, --help           show this help message and exit
      --only-interesting   Only log 'interesting' buckets whose contents match
                           anything within keywords.txt (default: False)
      --skip-lets-encrypt  Skip certs (and thus listed domains) issued by Let's
                           Encrypt CA (default: False)
      -t , --threads       Number of threads to spawn. More threads = more power.
                           (default: 20)

## F.A.Qs

- **Nothing appears to be happening**

   Patience! Sometimes certificate transparency logs can be quiet for a few minutes.

- **I found something highly confidential**

   **Report it** - please! You can usually figure out the owner from the bucket name or by doing some quick reconnaissance. Failing that contact Amazon's support teams.

## Contributing

1. Fork it, baby!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request.

## License

MIT. See LICENSE