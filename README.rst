mrjob
=====

mrjob is a Python package that helps you write and run Hadoop Streaming jobs.

mrjob fully supports Amazon's Elastic MapReduce (EMR) service, which allows you to buy time on a Hadoop cluster on an hourly basis. It also works with your own Hadoop cluster.

Some important features:

 * Run jobs on EMR, your own Hadoop cluster, or locally (for testing).
 * Write multi-step jobs (one map-reduce step feeds into the next)
 * Duplicate your production environment inside Hadoop
     * Upload your source tree and put it in your job's ``$PYTHONPATH``
     * Run make and other setup scripts
     * Set environment variables (e.g. ``$TZ``)
     * Easily install python packages from tarballs (EMR only)
     * Setup handled transparently by ``mrjob.conf`` config file
 * Automatically interpret error logs from EMR
 * SSH tunnel to hadoop job tracker on EMR
 * Minimal setup
     * To run on EMR, set ``$AWS_ACCESS_KEY_ID`` and ``$AWS_SECRET_ACCESS_KEY``
     * To run on your Hadoop cluster, install ``simplejson`` and make sure ``$HADOOP_HOME`` is set.

Installation
============
``python setup.py install``

Setting up EMR on Amazon
========================

 * create an Amazon Web Services account: <http://aws.amazon.com/>
 * sign up for Elastic MapReduce: <http://aws.amazon.com/elasticmapreduce/>
 * Get your access and secret keys (go to <http://aws.amazon.com/account/> and click on "Security Credentials")
 * Set the environment variables ``$AWS_ACCESS_KEY_ID`` and ``$AWS_SECRET_ACCESS_KEY`` accordingly

Try it out!
===========

::

    # locally
    python mrjob/examples/mr_word_freq_count.py README.md > counts
    # on EMR
    python mrjob/examples/mr_word_freq_count.py README.md -r emr > counts
    # on your Hadoop cluster
    python mrjob/examples/mr_word_freq_count.py README.md -r hadoop > counts

Advanced Configuration
======================
To run in other AWS regions, upload your source tree, run ``make``, and use 
other advanced mrjob features, you'll need to set up ``mrjob.conf``. mrjob looks 
for its conf file in:

 * ``~/.mrjob``
 * ``mrjob.conf`` anywhere in your ``$PYTHONPATH``
 * ``/etc/mrjob.conf``

See ``mrjob.conf.example`` for more information.


Links
=====

 * source: <http://github.com/Yelp/mrjob>
 * documentation: <http://packages.python.org/mrjob/>
 * Hadoop MapReduce: <http://hadoop.apache.org/mapreduce/>
 * Elastic MapReduce: <http://aws.amazon.com/documentation/elasticmapreduce/>
