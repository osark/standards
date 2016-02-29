Send Multi part Mail in Drupal 7/8
==================================

Resources
---------

-  `How to Avoid Spam
   Filters <http://help.pardot.com/customer/portal/articles/2128167-spam-filters-and-how-to-avoid-them>`__
-  `Reach More People and Improve Your Spam
   Score <https://litmus.com/blog/reach-more-people-and-improve-your-spam-score-why-multi-part-email-is-important>`__
   .
-  `Syntax of
   boundary <http://stackoverflow.com/questions/4656287/what-rules-apply-to-mime-boundary>`__
   .
-  `Multipart Content
   Type <https://www.w3.org/Protocols/rfc1341/7_2_Multipart.html>`__ .

Why Multi-Part Email is Important
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Most of Emails reported as spam and not deliver to client mail, So
   there was steps you must follow when you send email to limit spam
   score and the Preference is use ``multipart/alternative`` as content
   type then Separate your mail body in two content types first one is
   ``text/plain`` this is for Client Applications that's not Support or
   Cannot Parse HTML tags and the other is ``text/html`` for Client
   Applications that's support HTML but the priority for ``text/html``
   if Client Application able to parse HTML tags .

Implementation in Drupal 7
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    drupal_mail('module_name', 'TEST_SMTP', 'client@example.com', 'en' ,['key' => 'value']);

    -  Implementation in drupal 7 like drupal 8 , the only difference
       that drupal 7 using ``drupal_mail`` function and in drupal 8 you
       must get mail manager service to send mails .

Implementation in Drupal 8
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    class DefaultController implements ContainerAwareInterface {
        
        /** @var MailManager */
        protected $mailManager;
        
        /* dependcy injection */
        public function setContainer(ContainerInterface $container = null) {
            $this->mailManager = $container->get('plugin.manager.mail');
        }
        
        public function testSendMailAction() {
            $this->mailManager->mail('module_name', 'TEST_SMTP', 'client@example.com', 'en' ,['key' => 'value']);
            return [
                '#type' => 'markup',
                '#markup' => 'This Page In development '
            ];
        }
        
    }

    ``class DefaultController implements ContainerAwareInterface`` \*
    Implementing ContainerAwareInterface to inject mail service into
    Controller, also you can extend ControllerBase if you need but in
    this case we don't\` need to extend BaseController class.

    ``$this->mailManager = $container->get('plugin.manager.mail');`` \*
    this line to get mail manager service

    ``$this->mailManager->mail('module_name', 'TEST_SMTP', 'client@example.com', 'en');``
    \* It's very simple to use, First parameter is your module name to
    call hook\_mail , Second parameter is the key that use in hook\_mail
    to specify content , Third parameter is client mail and you can add
    more than one email by using comma separator (,) between emails ,
    'en' this is the encode of email ,and last parameter for sending
    parameters as associative array that will receive in hook\_mail

-  Now open your ``module_name.module`` file and implement hook\_mail
   function

.. code:: bash

    function module_name_mail($key, &$message, $params) {

      $message['from'] = \Drupal::config('system.site')->get('mail');
      $Plainttext = "Plaint Text Part";
      $HTMLpart = "<h1>HTML Part</h1>";
      switch($key)
      {
        case 'TEST_SMTP' :
          $message['subject'] = 'Test Email from Opensource Wiki';
          $message['headers'] = array(
            'MIME-Version' => '1.0',
            'Content-Type' => "multipart/alternative", 
            'Content-Transfer-Encoding' => '8Bit',
            'X-Mailer' => 'Drupal'
          );
          $message['body'][] = "\r\n--\r\n";
          $message['body'][] = 'Content-Type: text/plain; charset=utf-8;';
          $message['body'][] = "$Plainttext";
          $message['body'][] = "\r\n--\r\n";
          $message['body'][] = "Content-Type: text/html; charset=utf-8;";
          $message['body'][] = "$HTMLpart";
          $message['body'][] = "\r\n-- --\r\n";
          break;
      }

    }

-  This is the important part in your code to send mail .

    ``$message['from'] = \Drupal::config('system.site')->get('mail');``
    \* To specify the sender email address by this Code and we always
    use system site email (you can change this to any email as you like)

    ``$message['subject'] = 'Test Email from Opensource Wiki';`` \* set
    subject of email

    ``$message['headers'] = array(     'MIME-Version' => '1.0',     'Content-Type' => "multipart/alternative",     'Content-Transfer-Encoding' => '8Bit',     'X-Mailer' => 'Drupal' );``
    \* set headers of email and make sure you are set content type as
    multipart/alternative

    ``['body'][] = "\r\n--\r\n"; $message['body'][] = 'Content-Type: text/plain; charset=utf-8;'; $message['body'][] = "$Plainttext"; $message['body'][] = "\r\n--\r\n"; $message['body'][] = "Content-Type: text/html; charset=utf-8;"; $message['body'][] = "$HTMLpart"; $message['body'][] = "\r\n-- --\r\n";``
    \* You must add boundary code before and after each content type but
    it is not required to do that if you are using PHP\_Mailer Library
    this part to set plain text and HTML tags (syntax is very important
    check Resources)

    ``$message['params']['attachments'][] = array(     'filecontent' => file_get_contents(PATH_OF_FILE),     'filename' => 'file_name.extention',     'filemime' => 'application/type', );``
    \* To attach files use this code

*NOTES*:

-  Some library or PHP native needs to encode your file after using
   file\_get\_contents function , check your library requirements.
-  Email Client Applications use base64\_decode to decode attachment as
   default .
-  Download and enable `SMTP <https://www.drupal.org/project/smtp>`__
   Module then enter your SMTP configuration from
   ``http://host/config/system/smtp`` .
-  Change mailing system by this command
   ``drush cset system.mail interface.default SMTPMailSystem`` .

