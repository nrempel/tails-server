# VON Tails Server

> This softare is designed to run on linux kernel 3.11 or newer.

## Running Locally

From the docker directory, run `./manage start GENESIS_URL=http://test.bcovrin.vonx.io/genesis`.

## Usage

This server has two functions:

- Uploading a tails file
- Downloading a tails file

### Uploading

To upload a tails file, make a `PUT` request to `/{revoc_reg_id}` with the contents of the file. The Content-Type header must be set to `application/octet-stream`.

The server will lookup the relevant revocation registry definition and check the integrity of the file against `fileHash` on the ledger. If it's good, it will store the file. Otherwise it will respond with response code `400`. If `revoc_reg_id` does not exist on the ledger, the server will respond with response code `404`. If the file already exists on the server, it will respond with response code `409`.

### Downloading

A simple `GET` request will download a tails file. The path is `/{revoc_reg_id}` where `revoc_reg_id` is a valid id. If it doesn't exist, the server will respond with response code `404`.