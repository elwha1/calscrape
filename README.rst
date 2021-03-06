================================================
CalScrape: Scrape & Search Judicial Hearing Data
================================================


**CalScrape** is a free and open-source command line tool written in Python
that allows users to rapidly find data about hearings in certain US courts. In
other words, it is a judicial *cal* -endar *scrape* -er.


Why?
====

Data about judicial proceedings can be tricky to find and a pain to search
through. Records in the supposedly public PACER system cost an exorbitant
amount of money, and other solutions focus on providing full court dockets or
judicial opinions. Court websites, meanwhile, tend to spread the information
out over multiple pages or store it in a not-so-user-friendly format.

In short, there hasn't been an easy way for journalists or other interested
members of the public to find information about *upcoming* hearings that they
may want to attend. And that's important: open information about public
hearings helps ensure the proper functioning of the justice system.

.. epigraph::

    "The value of openness lies in the fact that people not actually attending
    trials can have confidence that standards of fairness are being observed;
    the sure knowledge that anyone is free to attend gives assurance that
    established procedures are being followed and that deviations will become
    known."

    -- `Press-Enterprise Co. v. Superior Court (1986)`_

.. _Press-Enterprise Co. v. Superior Court (1986): https://www.law.cornell.edu/supremecourt/text/478/1


Quickstart
==========

CalScrape is not yet available via PyPI. The easiest way to install it is to
clone the GitHub repo and use ``pip`` to resolve the dependencies. Assuming
you're on a Linux or other *nix-like system, open a terminal and enter:

.. code:: bash

   $ git clone https://github.com/elwha1/calscrape.git


Once you've done that, ``cd`` into the repo directory and install like so:

.. code:: bash

   $ pip install --user .


You will see ``pip`` fetch and install any necessary packages. Now, you should
be able to enter the following command to start using CalScrape:

.. code:: bash

   $ calscrape --help       


The same general process should also work on Windows (I just haven't tested it,
yet). Note that ``calscrape`` requires Python 3.6 or higher. If your system
ships with Python 2 as the default, you may need to change the ``pip`` command
to ``pip3`` after installing the latest version of Python.


Usage
=====

CalScrape currently has one big limitation: it only provides data from the
District Court for the North District of California in San Francisco. That
said, work has been done to keep the codebase modular enough to bolt on parsers
for additional courts with relative ease. This being an open-source project,
feel free to suggest courts that you think should be added!

When you run ``calscrape`` on the command line, your machine interacts with the
court's website. In general, it runs very fast. However, in order not to cause
any unintentional bottleneck in web traffic, the scraper is configured to wait
a bit before making each request.

CalScrape has several "modes" that can be invoked by passing different
arguments on the command line. These are ``--new``, ``--cancelled``,
``--showall``, and ``--find``. These are *mostly* self-explanatory, but the
behavior of the first two options bears some explanation.

When you run ``calscrape`` for the first time on your computer, it has no data
to compare against in order to determine which hearings are "new" or which have
been "cancelled". After you run it, the program will store a simple JSON file
in your home directory called ``calscrape_latest_scrape.json``. This file is
updated on each run. Now, you can pass the arguments to detect new or cancelled
hearings. You can think of the ``--new`` flag as showing hearings that are "new
to you," as in, they haven't been seen by your machine before -- and likewise
with the ``--cancelled`` flag.

Note, both the ``--new`` and ``--cancelled`` flags will output a stream of JSON
data about the hearings to ``stdout``. The default behavior when running
``calscrape`` with only the ``--court`` argument is simply to update the
``calscrape_latest_scrape.json`` file. The assumption is that if you want to
search through these data files, or store the data, you will use other
tools. (Check the GitHub issues to see what else is on the roadmap; adding
support for iCal and csv formats for data output is under consideration.)

By contrast, using the ``--find`` or ``--showall`` flags will show hearings in
a human-readable format. ``--find`` takes a single word or a phrase enclosed in
quotes as a search term to look through hearing captions; ``--showall`` does
just what you might think it would do -- show *all* the hearings on the calendar.


Contributing
============

CalScrape is an open source project being developed to further the public
interest and increase awareness about the court system. Contributions are
welcome. If you encounter an issue, please file it using the issue-tracking
tool. If you'd like to contribute or have ideas for how to improve CalScrape,
feel free to make a pull request.


License
=======

In order to adhere to the mission of keeping court data free and open to the
public, CalScrape is licensed under the GNU Affero General Public License. For
more details, see the LICENSE.txt file.
