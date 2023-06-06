---
slug: "gotcha-with-exporting-mysql-tables-for-windows"
title: Gotcha with exporting MySQL tables for windows
date: "2013-01-09"
tags: ['carriage return', 'encoding', 'latin1', 'mysql', 'perl', 'unicode', 'utf']
---
I encountered some interesting issues when pulling out CSV from my MySQL databases. The core issue was the csv generated was not seemingly compatible with the various spreadsheet readers in Windows. After having a closer look at the file, it turns out to be an encoding issue clearly.

As the database was Latin1 encoded, the carriage return was handled as r [shows up as ^M on VI] in some text blobs. That basically resulted in an additional carriage return in the reader and it would break the csv. Here was the way I solved this issue.

perl -pie ’s/r//g’ *.csv

This will basically remove all the r  and thus ensure that your reader is able to accept and read the file. You should be able to see the difference when you export the file into the reader.
