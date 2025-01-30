# Bitcoin Cash Mainnet

The mainnet of Bitcoin Cash is the network that operates on the Bitcoin Cash blockchain. 

The mainnet is the official blockchain (there are also `testnets`, `scalenet` and `regtest`), however this repository only looks at the mainnet.

## Synchronize with the Mainnet

There are two ways to retrieve the mainnet data:

- Synchronize using a Bitcoin Cash node (preferred method)
- Downloading a mainnet snapshot

### Synchronize Bitcoin Cash node

You can use any node software that works on the Bitcoin Cash network in order to retrieve the mainnet blockchain data. Such a Bitcoin Cash client is called a full node. 

This is actually the **recommended way of getting the blockchain data**.  Depending on your hardware, synchronizing the full node can take quite a while.

### Downloading a mainnet snapshot

Alternatively, you can also download _a snapshot_ from the mainnet. 

The benefit of downloading a snapshot is that downloading might be faster than trying to synchronize the full blockchain from the Bitcoin Cash network from scratch. Depending on your computer / server hardware specification, the synchronization duration may vary.

Just understand that there is also a downside of downloading the mainnet. The downside is that you have to trust the author (Melroy van den Berg) for publishing the Bitcoin Cash blockchain mainnet data. However, I signed the `tar.zst` file so you can verify the compressed file yourself. This mainnet data also contains `txindex` and `coinstatsindex`.

- [Download Bitcoin Cash mainnet 2025-01-25](./downloads/bitcoin_cash_mainnet_2025-01-25_txindex.tar.zst.torrent)

After you have downloaded the mainnet data, you will need to uncompress the data via:

```sh
tar --zstd -xvf bitcoin_cash_mainnet_2025-01-25_txindex.tar.zst
```

Finally, you can copy the mainnet data directly to the [Data Directory](https://docs.bitcoincashnode.org/doc/bitcoin-conf/#configuration-file-path). Eg. `~/.bitcoin` under GNU/Linux. 

Once you start the Bitcoin Cash Node, the remaining data will be synchronized and the node should be fully in-sync in no time. Good luck!

#### Verify the compressed file

After you downloaded the file above, you could verify that I ([Melroy van den Berg](https://gitlab.melroy.org/-/snippets/487)) signed the `.tar.zst` file using my PGP private key by validating against [my GnuPG public key](https://keys.openpgp.org/search?q=E0C7C029005B0CE6A7438BD571D11FF23454B9D7).

1. Retrieve the PGP key:

```sh
gpg --keyserver keys.openpgp.org --recv-keys E0C7C029005B0CE6A7438BD571D11FF23454B9D7
```

2. Verify fingerprints:

```sh
gpg --fingerprint E0C7C029005B0CE6A7438BD571D11FF23454B9D7
```

Output should show:

```sh
pub   rsa3072 2021-04-06 [SC]
      E0C7 C029 005B 0CE6 A743  8BD5 71D1 1FF2 3454 B9D7
uid           [ unknown] Melroy Antoine van den Berg <melroy@melroy.org>
sub   rsa3072 2021-04-06 [E]
```

3. Download the signature (`.asc`) file:

- [Bitcoin Cash mainnet 2025-01-25 signature](./downloads/bitcoin_cash_mainnet_2025-01-25_txindex.tar.zst.asc)

4. Copy/move the signature (`.asc`) file, from step 3, to the **same directory** as the other `.tar.zst` file. Assuming the torrent download is completed.

5. Verify the signature of the download, by executing:

```sh
gpg --verify bitcoin_cash_mainnet_2025-01-25_txindex.tar.zst.asc bitcoin_cash_mainnet_2025-01-25_txindex.tar.zst
```

The output should say "Good signature from "Melroy Antoine van den Berg melroy@melroy.org"":

```sh
gpg: Signature made Wed 07 Apr 2021 12:51:23 AM CEST
gpg:                using RSA key E0C7C029005B0CE6A7438BD571D11FF23454B9D7
gpg: Good signature from "Melroy Antoine van den Berg <melroy@melroy.org>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg: There is no indication that the signature belongs to the owner.
```

Notice that there is a warning because you haven't assigned a trust index to this person (_which can be ignored!_).


```sh
gpg: WARNING: This key is not certified with a trusted signature!
gpg: There is no indication that the signature belongs to the owner.
```

This means that GnuPG verified that the key made that signature, but it's up to you to decide if that key really belongs to the developer. The best method is to meet the developer in person and exchange key fingerprints.

Ps. I attend [FOSDEM](https://fosdem.org) each year, if you really want, you can meet me in person and exchange keys.
