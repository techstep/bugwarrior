Jira
====

You can import tasks from your Jira instance using
the ``jira`` service name.

Example Service
---------------

Here's an example of a jira project::

    [my_issue_tracker]
    service = jira
    jira.base_uri = https://bug.tasktools.org
    jira.username = ralph
    jira.password = OMG_LULZ

.. note::

   The ``base_uri`` must not have a trailing slash.

The above example is the minimum required to import issues from
Jira.  You can also feel free to use any of the
configuration options described in :ref:`common_configuration_options`
or described in `Service Features`_ below.

Service Features
----------------

Specify the Query to Use for Gathering Issues
+++++++++++++++++++++++++++++++++++++++++++++

You can specify the query used for gathering issues by using the
``jira.query`` parameter.  For example, to select issues assigned to
'ralph' having a status that is not 'closed' and is not 'resolved', you
could add the following configuration option::

    jira.query = assignee = ralph and status != closed and status != resolved

Jira v4 Support
+++++++++++++++

If you happen to be using a very old version of Jira, add the following
configuration option to your service configuration::

    jira.version = 4


Import Labels as Tags
+++++++++++++++++++++

The Jira issue tracker allows you to attach labels to issues; to
use those labels as tags, you can use the ``jira.import_labels_as_tags``
option::

    jira.import_labels_as_tags = True

Also, if you would like to control how these labels are created, you can
specify a template used for converting the Jira label into a Taskwarrior
tag.

For example, to prefix all incoming labels with the string 'jira_' (perhaps
to differentiate them from any existing tags you might have), you could
add the following configuration option::

    jira.label_template = jira_{{label}}

In addition to the context variable ``{{label}}``, you also have access
to all fields on the Taskwarrior task if needed.

.. note::

   See :ref:`field_templates` for more details regarding how templates
   are processed.

Provided UDA Fields
-------------------

+---------------------+---------------------+---------------------+
| Field Name          | Description         | Type                |
+=====================+=====================+=====================+
| ``jiradescription`` | Description         | Text (string)       |
+---------------------+---------------------+---------------------+
| ``jiraid``          | Issue ID            | Text (string)       |
+---------------------+---------------------+---------------------+
| ``jirasummary``     | Summary             | Text (string)       |
+---------------------+---------------------+---------------------+
| ``jiraurl``         | URL                 | Text (string)       |
+---------------------+---------------------+---------------------+
