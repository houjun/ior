Release Process
===============

To build a new version of IOR::

    $ docker run -it ubuntu bash
    $ apt-get update
    $ apt-get install -y git automake autoconf make gcc mpich
    $ git clone -b rc https://github.com/hpc/ior
    $ cd ior
    $ ./travis-build.sh

To create a new release candidate from RC,

1. Disable the ``check-news`` option in ``AM_INIT_AUTOMAKE`` inside configure.ac
2. Append "rcX" to the ``Version:`` field in META where X is the release
   candidate number
3. Build a release package as described above

To create a new minor release of IOR,

1. Build the rc branch as described above
2. Create a release on GitHub which creates the appropriate tag
3. Upload the source distributions generated by travis-build.sh

To create a micro branch of IOR (e.g., if a release needs a hotfix),

1. Check out the relevant release tagged in the rc branch (e.g., ``3.2.0``)
2. Create a branch with the major.minor name (e.g., ``3.2``) from that tag
3. Update the ``Version:`` in META
4. Apply hotfix(es) to that major.minor branch
5. Create the major.minor.micro release on GitHub

To initiate a feature freeze,

1. Merge the master branch into the rc branch
2. Update the ``Version:`` field in META `of the master branch` to be the `next`
   release version, not the one whose features have just been frozen
