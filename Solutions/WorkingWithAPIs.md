# Working with APIs & Real-World Data — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/WorkingWithAPIs.md](../Lessons/WorkingWithAPIs.md). Try each question yourself before reading the answer.

1. `200` means the request succeeded. `4xx` codes mean something's wrong with **your** request (a bad parameter, missing authentication, a URL that doesn't exist — `404`). `5xx` codes mean something's wrong on the **server's** end (their code crashed, their service is overloaded) — not something you did.

2. A raw nested dict passed straight into `pd.DataFrame()` often produces a DataFrame where some cells contain entire dicts or lists as their value, instead of separate columns — not usable for normal column-based analysis. `pd.json_normalize()` walks the nested structure and flattens it, turning `{"address": {"city": "Austin"}}` into a proper column named `address.city` with a plain string value.

3. A failed request still returns *something* in the response body — often an error page or an error-describing JSON object, not the data you wanted. If you call `.json()` without checking the status first, you can end up silently treating that error content as if it were real data, which produces confusing bugs much later (a `KeyError` on a field that was never there, or garbage values) instead of a clear, immediate failure at the point where the actual problem happened.
