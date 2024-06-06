# DDISExercise4
Github repo to show the code used in exercise 4 of DDIS


**Exercise 4**

**CockroachDB**

**SETUP**

|                                         |                   |
| :-------------------------------------: | :---------------: |
|             **API platform**            | Google cloud run  |
|         **Programming language**        |       Python      |
|   **(Micro)Framework used for server**  |       Flask       |
|          **DB Driver library**          |     Psycopg 3     |
| **Platform for testing API requests**   |      Postman      |

- **Exposing the IP of a pod with a load balancer so that the DB drivers from outside can connect to it.**

****![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeXVWUQ3l2J2TtJV96v_NyKNOREyTS9FkpRo21xbS0u1UPlYG1xi5OMWL62MQ-6eavng787huq2wigYgqWaiKXqGBmBAlbwPaGIMMJoTZl6NcvKMYzP0gAlIK2ZxqPM331NlVgANIoe1TNxxzGOX7HrGled?key=07PbvhN_YYcUfuFBLacp3g)****

- **Building docker image, tagging it and pushing it to the artifact registry.**

|                                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------- |
| docker build -t python-flask . docker tag python-flask docker push europe-west1-docker.pkg.dev/testprojectddis/dockerrepo/python-flask |

- **Creating a service which runs a container created from the docker image pushed above.**

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXexTzrBr5dvhD1Sfq1xAl67fIgp9ndyTFKb0dg5JmXUKvZv2hZR6mZgXeGIcWnYit3pDcLqhPRHlCpKoDoxnvchPMk40ZzXZKGYRMYRtAR8M-L67ZIOCUqh6j3hQ3S4_yFBbblzlINBh-5sLSgk8qhegM6_?key=07PbvhN_YYcUfuFBLacp3g)

**Use cases**

**(1)** **Login**

User authenticates by email and password. Returns a token in JWT format

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfZoyoSX4iM2Jos5MCS5G8CIEnujDOI3yvwx8ndgkw_uX8Fxcvaj8gIyVjcwil9e065XXDPVeEaqj97tU9YE3xDuU2kKAf_j4gbXXpxGKWJcHLaZkg5N7Q2fDi8TU_iD6_moirunhhMwj2S6u8Ix1xejjYY?key=07PbvhN_YYcUfuFBLacp3g)

**(2) Get user details by user id**

Returns all user attributes (without password) for a specified user id that is provided by the request (may be ≠ authenticated user id as in token).

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdbTttHaq1tGlcoHjp1NulIZi2NIUmJQbDvZ6Std-B8Kl0l2-7nIfjrmansJExT3l-zrbMN446CNrhbIfowVq9Q3DOmksKtjhUMX0Ls7jJDFqKcr_ygmonYlbonA493O6iTazyzbmL6QnjcySdOpI2D_8o4?key=07PbvhN_YYcUfuFBLacp3g)

**(3) List sales by user id**

Returns all sales of a specified user. May be filtered by item title, seller description, and manufacturer description. Ordered descending by date offered.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeBTCVy3BYAQLEkheP7DuHHbgNjd8BkAo7ZkO-vvyBQRYeJzxYrUyT1QM2pKEDW-GAbYzBUCTFrdyghBelqc-y-e3Nu1Y6nQb8sywYQVwYXH61qS3No-Xrk59vzk0mq6Jy5TYKuOrRQF5jnjdUIvOa8IYI?key=07PbvhN_YYcUfuFBLacp3g)

**(4) List purchases by user id**

Same as (3) for purchases instead of sales.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcgvCv5pfbE8TAa8xSuD45YMyc8L4MvsfG53WGdSR7pLm-P5TqY7butr83lPUw_gkdbzqSLc7cM1u2VPeTVkwB8a1y0GH3q_7GGbjLuqk8S-xtJJNDCFqHgSNk9oe3-DMrN8vISgRvEKHWCJRd3-j0H5rxA?key=07PbvhN_YYcUfuFBLacp3g)

**(5) List offers by user id**

Returns all offers of a specified user.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdFtQmMHWiq4TgozWt2ZlXGYizUACdiuWyGNqP-LGWSMyu-hwWpkfDoXlDpcHnSGqilH7Us6EDWBh_l_j7xF1_t-q1gy34rMvq-vOIeYuwJC_ZCt4doyhNf6ljxWKczfxS-lALxkdpY-5oeHrs3m8fsQUs?key=07PbvhN_YYcUfuFBLacp3g)

**(6) List offers**

Returns selected offers of arbitrary users in an unspecified order, limited to the first 100.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcokErTbuEZnIxyeDX_9mQvbHr7SxQlG_6eROrVTCI0gVnzBRhZ-uES5mq5L_ZhUv8SfDHyaokm6DfZT0ivIBjOFLEKN7XxvZa-WRiXz0HFNK5KiiwH3Dgwsjirla3oevNab8OPboIdLEa3-ovPczcpRkRX?key=07PbvhN_YYcUfuFBLacp3g)

**(7) Create offer**

Creates and returns a new sales record with seller\_uid = authenticated user id as in token, buyer\_uid = null, date\_offered = now(), date\_sold = null, and all other attributes filled with valid random values.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfshKeR76qrzimac02zlOJXxwpw8LPfsjljdNLs4nibVTPrcTAQLVUi6FYNpnCqfoW2ZE162PhlKdIhUg5_ed6lDYX5ZfCB_XBNjn0YoWXva-iwE9fsiolMWoVrUePbqjSuzRTcX9dY-oF2ft4sJ1xlgGFz?key=07PbvhN_YYcUfuFBLacp3g)

**(8) Buy an offered item by sale id**

An authenticated user is not allowed to buy his own offers. This is a transaction as multiple records have to be updated.

The attributes buyer\_uid = authenticated user id as in token, and date\_sold = now() are set for the sales record.

The derived attribute sales of the referenced item record has to be updated.

The derived attributes sales, sales\_sum, and balance have to be updated for the referenced seller user record.

The derived attributes purchases, purchases\_sum, and balance have to be updated for the referenced buyer user record.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfS99qUsTSIbqGX03HwFpCzfom-eFdJdIyMD9pjRP3d3iIASaOS96Vf6vz0raT4gBX6N0uyDg2sD6jKbG7S9PTnYec-MtWxiihFcqD2MDQTZVOAfb32CFzNYcgxgQNQBevDNI5vaq2noecmGpi6sD2kOsST?key=07PbvhN_YYcUfuFBLacp3g)


**(9) Delete offer by sale id**

An authenticated user is only allowed to delete his own offers

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXc8Gnk4cTfK-n5Tx15_hNOTLrPj7cvzY88uqBqJqnbLg-vkCppyZXt4MJMqnfcH8PsONq0Q_lD-1wfhCVNDLLvNh6QrwN3Ji5mylvHnCAeA51UKqbAymhINXkyy-J1k_AWlHcE8RESapF1hnawSmqmVJROR?key=07PbvhN_YYcUfuFBLacp3g)

The following failures should by handling by adequate response codes, e.g. 401, 403, 404:

− Incorrect credentials: (1)

− Invalid user token: (2) – (9)

− Unknown user id: (2) – (5)

− Unknown sale id: (8) – (9)

− Unauthorized: (8) – (9)

− Invalid data: (7)

**Issues faced:** 

- Google cloud run sticks to best REST API practices so GET requests are not allowed to have a json body apart from query params. Changing to PUT could have fixed that but changed the way of getting data to query params instead of json body. 

- Minor issues in authorising with artefact registry to push the docker image.

- Connecting with DB. Had to expose the pod explicitly in google cloud console so that DB driver can connect to it properly.
