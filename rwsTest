.. _update-subject-data:

Feature: Working with subject data
==================================

Scenario
--------

  *As an integrating system*

  *I want to update my subjects data*

  *So that I can manage my clinical data*

[:ref:`examples <examples-post-clinical-data>`]

[:ref:`best practices <update-subject-data-best-practices>`]


Assumptions
-----------

To succeed, I have satisfied these pre-requisites:

#. I am a valid Rave User
#. I can update clinical data in my study
#. My subject exists in my study and can be updated
#. The fields pre-conditions for my role have been met
#. My Request body does not exceed the maximum request size of 1,000,000 bytes


.. note::
  To record a change code for field updates, the first change code associated with a user's role in Rave is used.
  If the user's role does not have a change code, no change code is used.


My POST Request
----------------

Header
^^^^^^^^^^^

My header contains the following elements:

#. :ref:`My authentication <authentication>`
#. A valid Content-type of "text/xml" or "text/xml; charset=UTF-8;"


URI
^^^^^^^^^^^
::

  POST https://{host}/RaveWebServices/webservice.aspx?PostODMClinicalData


URI Parameters:

+--------------------------+--------------------------------+------------+------------------------------+
| Parameter                | Description                    | Mandatory? | Notes                        |
+==========================+================================+============+==============================+
| {host}                   | The host name                  | Yes        | usually "{client}.mdsol.com" |
+--------------------------+--------------------------------+------------+------------------------------+


Example::

  POST https://my-organisation.mdsol.com/RaveWebServices/webservice.aspx?PostODMClinicalData

.. note::  PostODMClinicalData is case sensitive.


Body
^^^^^^^^^^^

My request Body is a :ref:`valid ODM 1.3 transactional document <valid-odm-transactional-document>`

My ODM document is constructed as follows [#Footnotes1]_:

.. code-block:: xml

    <?xml version="1.0" ?>
    <ODM  >

      <!-- "Field location Attributes" -->

      <ClinicalData StudyOID="{study-oid}" >
        <SubjectData SubjectKey="{subject-key}" TransactionType="Update" >
          <SiteRef LocationOID="{location-oid}" />
          <StudyEventData StudyEventOID="{folder-oid}" StudyEventRepeatKey="{folder-repeat-key}" TransactionType="Update" >
            <FormData FormOID="{form-oid}" FormRepeatKey="{form-repeat-key}" TransactionType="Update" >
              <ItemGroupData ItemGroupOID="{record-oid}" ItemGroupRepeatKey="{item-group-repeat-key}" TransactionType="Update" >

                <!-- "Field level Attributes (with variations below)" -->

                <ItemData ItemOID="{field-oid}" Value="{data}" />

              </ItemGroupData>
            </FormData>
          </StudyEventData>
        </SubjectData>
      </ClinicalData>

    </ODM>


.. note::  I can only update one subject per request


Field location Attributes:

+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| Attribute           | Description                                         | Mandatory? | Notes                                               |
+=====================+=====================================================+============+=====================================================+
| StudyOID            | The study identifier                                | Yes        | See :ref:`Locating my study <locate-a-study>`       |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| SubjectKey          | The subject identifier                              | Yes        | See :ref:`Locating my subject <locate-a-subject>`   |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| LocationOID         | The site identifier                                 | Yes        | See :ref:`Locating my site <locate-a-site>`         |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| StudyEventOID       | The folder OID or "SUBJECT" for subject level forms | Yes        |                                                     |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| StudyEventRepeatKey | The folder repeat key                               | No         | See :ref:`Locating my folder <locate-a-folder>`     |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| FormOID             | The form OID                                        | Yes        |                                                     |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| FormRepeatKey       | The form repeat key                                 | No         | See :ref:`Locating my form <locate-a-form>`         |
|                     |                                                     |            | and :ref:`Upserting my form <upsert-a-form>`        |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| ItemGroupOID        | The form OID or form OID + "_LOGLINE"               | Yes        |                                                     |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| ItemGroupRepeatKey  | The log line repeat key or "1"                      | No         | See :ref:`Locating my log line <locate-a-log-line>` |
|                     |                                                     |            | and :ref:`Upserting my log line <upsert-a-log-line>`|
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+


Field level Attributes (with variations below):

+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| Attribute           | Description                                         | Mandatory? | Notes                                               |
+=====================+=====================================================+============+=====================================================+
| ItemOID             | The field OID                                       | Yes        | See below                                           |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+
| Value               | The data                                            | Yes        | See below                                           |
+---------------------+-----------------------------------------------------+------------+-----------------------------------------------------+


Inserting a new subject
^^^^^^^^^^^^^^^^^^^^^^^^^^

I can create a subject, and add data to it:

* :ref:`Creating my subject in a study and site <create-a-subject>`


Updating Field data:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I can update fields of these data types, control types and properties:

* :ref:`Text field <text-field>`
* :ref:`Date field <date-field>`
* :ref:`Unit dictionary field <unit-dictionary-field>`
* :ref:`Data dictionary drop down list <data-dictionary-drop-down-field>`
* :ref:`Data dictionary search list <data-dictionary-search-list-field>`
* :ref:`Data dictionary dynamic search list <dynamic-search-list-field>`

I can update these properties on a field:

* :ref:`Workflow properties <workflow-for-fields>` - Lock, Freeze, Verify

I can not update:

* Other workflow properties - Sign
* Derived fields, such as "Age".


Updating items belonging to a field:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I can update these field items:

* :ref:`Review <field-review>`
* :ref:`Queries <field-queries>` - Open, Forward, Answer, Cancel, Close
* :ref:`Translations <field-translations>`
* :ref:`Coding decisions <field-coding-decisions>`
* :ref:`External audits <field-external-audits>`

I cannot update:

* Comments
* Stickies
* Protocol Deviations


[:ref:`examples <examples-post-clinical-data>`]

[:ref:`best practices <update-subject-data-best-practices>`]


The Response
----------------

My whole transaction will either:

A. Succeed with a HTTP Response code of 200 OK;
B. Fail and roll back, with a 4xx or 5xx HTTP Response code and RWS error code in the response body.

+--------+----------------------+-------------------------------------------+------------------------------+
| Header | Reason               | Body                                      | Notes                        |
+========+======================+===========================================+==============================+
| 200    | The transaction      | XML representation of the items touched   | See Response Notes for more  |
|        | was successful       |                                           | information on the returned  |
|        |                      |                                           | XML.                         |
+--------+----------------------+-------------------------------------------+------------------------------+
| X      | Failure reason for X | response message                          | See :ref:`The Error Responses|
| Y      | Failure reason for Y |                                           | Listing <error-responses>`   |
| Z      | Failure reason for Z |                                           |                              |
+--------+----------------------+-------------------------------------------+------------------------------+


Example success response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Header::

  HTTP Response code : 200 OK


Body:

.. code-block:: xml

   <Response ReferenceNumber="fa63d085-629a-419e-a19d-21d6fb2bc93b"
    InboundODMFileOID="InputODM.xml"
    IsTransactionSuccessful="1"
    SuccessStatistics="Rave objects touched: Subjects=1; Folders=0; Forms=0; Fields=1; LogLines=0"
    NewRecords=""
    SubjectNumberInStudy="1"
    SubjectNumberInStudySite="1">
   </Response>


Example error response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Header::

  403 HTTP Response code

Body:

.. code-block:: xml

   <Response ReferenceNumber="fa63d085-629a-419e-a19d-21d6fb2bc93b"
    InboundODMFileOID="InputODM.xml"
    IsTransactionSuccessful="0"
    ReasonCode="RWS00042"
    ErrorOriginLocation="/ODM/ClinicalData[1]/SubjectData[1]/StudyEventData[1]/FormData[1]/ItemGroupData[1]/ItemData[1]"
    SuccessStatistics="Rave objects touched: Subjects=0; Folders=0; Forms=0; Fields=0; LogLines=0"
    ErrorClientResponseMessage="Field not authorised.">
   </Response>


.. rubric:: Footnotes

.. [#Footnotes1] Some attributes are omitted from the ODM document for clarity. See :ref:`ODM Schema <odm-schema>` for more details



