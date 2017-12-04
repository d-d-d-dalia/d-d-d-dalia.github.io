---
layout: post
title:      "Custom Attribute Writer and Nested Forms in Rails"
date:       2017-12-04 19:32:53 +0000
permalink:  custom_attribute_writer_and_nested_forms_in_rails
---


The custom attribute writer and the nested form in this project really had my brain swimming. This revelation that I can't reach the attribute of the join table from within a form without going *through* another attribute is really exciting! I had to create a *semi* - empty object first and then write to it by utilizing my access to another model from the starting point model. The exercise of thinking about what you have access to first is key. e.g. from the starting point within the form_for @song, I had to think about what I could reach using the Song model, and how to *get to* the attributes I wanted to write to in my form.

Associated build was key here.
