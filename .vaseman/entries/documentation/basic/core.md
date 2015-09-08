---

layout: documentation.twig
title: Core Concept

---

# MVC Groups

Every database table in phoenix will be separated to two MVC groups. One is singular item and another is plural list.
Every MVC group has it's own Model/View/Controller. For example, a table named: `sakuras`, we will use `Sakura` Controller
to modify single item record, and a `Sakuras` Controller to handle multiple items operation like `filter`, `ordering` or `batch update`.

# Definition

## Item

A Singular MVC group, used to handle CRUD of single record, shows the edit page.

## List

A plural MVC group, used to handle multiple items filter, ordering, batch update and copy etc. Shows a grid page or item list.

## Subsystem

Combine singular and plural two MVC groups, they are both maintains same database table.

# CRUD

CRUD means `Create` / `Read` / `Update` and `Delete` to one item record.

Phoenix use `save` to handle `create` and `update`. Se you will see `CrudModel` has only `save()` method instead `create()` and `update()`.

The save() method will determine that if data has primary key, it will use update process, if data has no primary key, then model will use create process.

# REST

Default RESTful methods has relations to CRUD operation:

| Method | Controller | Note |
| --- | ---- | --- |
| GET | READ | |
| POST | CREATE | |
| PUT | UPDATE | full fields |
| PATCH | UPDATE | partial fields |
| DELTE | Delete | |

## Method Controller Mapping

In Windwalker, we use this mapping to call controller.

| Method | Controller | Note |
| --- | ---- | --- |
| GET | GetController | |
| POST | SaveController | |
| PUT | SaveController | |
| PATCH | SaveController | |
| DELTE | DeleteController | |

It's more simpler to write your logic because you can use the exists of primary key to make create or update action.

## Grid & List Controller

In phoenix, we use this mapping to map list controller:

| Method | Controller | Note |
| --- | ---- | --- |
| GET | GetController | Show grid UI |
| POST | CopyController | Batch copy items |
| PUT | UpdateController | Batch update items |
| PATCH | Controller | Filter & search |
| DELTE | DeleteController | Delete items |


