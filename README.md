# Prerequisites
Run
```bash
sudo apt-get update

sudo apt-get install -y \
    build-essential \
    libreadline-dev \
    zlib1g-dev \
    flex \
    bison \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libpam0g-dev \
    libedit-dev \
    llvm-15 \
    llvm-15-dev \
    clang-15

sudo apt-get install pkg-config
sudo apt-get install libicu-dev
```
# Compile
- Get path of llvm-config tool: `which llvm-config-15`. Suppose the output is `/usr/bin/llvm-config-15`
- Install PostgreSQL in custom directory: 
```bash
git clone https://github.com/postgres/postgres.git
cd postgres
CLANG=/usr/bin/clang-15 LLVM_CONFIG=/usr/bin/llvm-config-15 ./configure --with-llvm
make -j$(nproc)
sudo make install

```

# Run with JIT
Modify `/usr/local/pgsql/data/postgresql.conf` and make sure `jit = on`.
Then run `pg_ctl -D data -l logfile start` to start the PostgreSQL server.
To verify the JIT, first run `psql` to enter into the DB session, then run `SHOW jit;`.
The expected output is:
```bash
 jit
-----
 on
(1 row)
```
