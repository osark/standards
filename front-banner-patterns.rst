Patterns for Website Banners
============================

Purpose
-------

A common request in modern Web sites to have some sort of graphical
banner, usually with some text inside. These are most important guide
lines for banners. These patterns are specially important for displaying
the banner image on different zoom levels or screens and always
displaying the main content.

Assumptions
-----------

-  The banner image is added as ``background-image`` property. Not
   ``<img>`` tag.
-  The design is flexible or responsive.

Banner Images
-------------

There are 3 important guide lines regarding image specifications: 1.
Image Size 2. Image Aspect Ratio 3. Image CSS properties

1. Image Size
~~~~~~~~~~~~~

| Focus on image **width**. It must match the maximum screen size
acceptable by client.
| Usually *1600 px* or *1900 px* are enough.

We will use ``background-size: cover`` property to always make sure that
the image width is 100% of the screen.

2. Image Aspect Ratio
~~~~~~~~~~~~~~~~~~~~~

Aspect ration affects image height. You should calculate the aspect
ration for image main content to be visible.

*For Example*: Image size is *1600 x 900 px*. So the aspect ratio is
*16:9* which is excellent for hight definition images.

| The banner image is usually visiable through *viewport*, a fixed width
and height ``<div>`` with the banner as background image.
| To determine the height of the *viewport*, you can calculate it based
on the *viewport* width.

Height Calculation
^^^^^^^^^^^^^^^^^^

| Don't use pixels ``px`` for height unit.
| On default zoom level, *1 screen* pixel matches *1 css* pixel. On
lower zoom level, *1 screen* pixel matches *more than 1 css* pixel. For
example: (50% Zoom level, 1 screen pixel = 2 css pixel)
| On heigher zoom level, *1 css* pixel matches *more than 1 screen*
pixel. For example: (200% Zoom level, 2 screen pixel = 1 css pixel)

Height Alternative
^^^^^^^^^^^^^^^^^^

Instead of using ``height`` css property, we will use ``padding`` on
parent *viewport*! ``padding`` property when given value in percentage
``%``, it's calculated as percentage of the parent container!!
(*Interseting CSS Feature*) To calculate the required padding, use the
following equation:

::

    Padding (Top OR Bottom)  = 100% x (aspect/ratio)^-1

*Example*: \* Aspect Ratio = **16:9** => padding-bottom = 100% \* 9/16 =
**56.25%** \* Aspect Ratio = **4:3** => padding-bottom = 100% \* 3/4 =
**75%**

3. Image CSS properties
~~~~~~~~~~~~~~~~~~~~~~~

Image is used as ``background-image`` property. Image is centered and
stretched.

.. code:: html

    <div class="viewport>
      <div class="banner-img"></div>
    </div>

.. code:: css

    .viewport {
      position: relative;
      padding-bottom: 56.25%; /* (100% x 9/16) */
      height: 0; /* Only height
    }
    .banner-img {
      position: absolute;
      left: 0;
      right: 0;
      height: 100%;
      background-position: center center;
      background-repeat: no-repeat;
      background-color: transparent;
      background-size: cover;

      /* Dont't forget background-image! */
    }

Example
-------

-  See BannerPatterns.html in project files.

Special Cases
-------------

-  Notice if you need to include text inside the banner image, it will
   change in size as you zoom in and out. And it might overflow the
   *viewport*.
-  If you have scallable content above the *viewport*, the *viewport*
   will move up and down as you zoom in and out.
-  For really small screens, you can move the content inside the banner
   image outside. (For example, remove the position absolute for inside
   content)

