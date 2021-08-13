---
title: Creating Efficient Queries
description: The following table identifies important concepts to consider when creating an efficient query.
ms.assetid: 1eb92d74-0a17-43f9-b5bf-eed731a52551
ms.tgt_platform: multiple
keywords:
- Active Directory examples Active Directory , creating efficient queries
ms.topic: article
ms.date: 05/31/2018
---

# Creating Efficient Queries

The following table identifies important concepts to consider when creating an efficient query.



| Area                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Indexing              | Ensure that the query filter contains at least one indexed attribute.<br/> For more information, see [Indexed Attributes](indexed-attributes.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Class vs. Category    | The statement "objectClass=xyz" refers to directory objects in which "xyz" represents any class in the object class hierarchy, whereas "objectCategory=xyz", refers to those directory objects in which "xyz" identifies a specific class in the object class hierarchy. The [**objectClass**](/windows/desktop/ADSchema/a-objectclass) property can take multiple values, whereas [**objectCategory**](/windows/desktop/ADSchema/a-objectcategory) takes a single value and is, thus, better suited for type matching of objects in a directory search.<br/>                                                                                                                                                                                          |
| Text searching        | Avoid searching for text in the middle and on the end of a string.<br/> For example, "cn=\*hille\*" or "cn=\*larouse".<br/> Using more specific matching criteria tends to increase search performance. This is because Active Directory Domain Services will evaluate all predicates, identifies the indices, and then chooses one index most likely to yield the smallest set of returned values. This technique does not work well with mid- and end-string searches. If you have no other option other than using these searches, you can define a tuple index for the attribute.<br/> For more details about tuple indexes see [How Tuple Indexing Works](how-tuple-indexing-works.md).<br/> |
| Subtree searching     | Use the global catalog if you are considering subtree searches. Chasing referrals requires extensive resources.<br/> For more information, see [Specifying Other Search Options](specifying-other-search-options.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Use of paging         | Assume that a subtree search will return a large result set. Use paging when performing subtree searches. The server will stream a large result set in chunks reducing the server side memory resources. This minimizes network usage and reduces the need for sending large chunks of data over a network.<br/> For more information, see [Specifying Other Search Options](specifying-other-search-options.md).<br/>                                                                                                                                                                                                                                                                                        |
| Combine searches      | Use multiple attributes for a search. One search of an object that reads two attributes is more efficient than two searches of the same object, each returning one attribute.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Efficient use of bind | Bind to an object one time and hold the binding handle for the rest of the session. Do not bind and unbind for each call. If you use ADO or OLE DB, do not create many connection objects.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| RoodDSE caching       | Read the rootDSE one time and remember its contents for the rest of your session.<br/> For more information, see [Serverless Binding and RootDSE](serverless-binding-and-rootdse.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Reference persistance | Persist references to objects as GUIDs, not distinguished names, in order to be rename and delete safe.<br/> For more information, see [Using objectGUID to Bind to an Object](using-objectguid-to-bind-to-an-object.md).<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |



 

 
