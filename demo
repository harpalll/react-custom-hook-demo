import { useEffect, useState } from "react";

const useFetch = (url, method = "GET", body = null, headers = {}) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);
        const isBodyAllowed = method !== "GET" && method !== "HEAD";

        const options = {
          method,
          headers: isBodyAllowed
            ? { "Content-Type": "application/json; charset=UTF-8", ...headers }
            : headers,
        };

        if (isBodyAllowed && body) {
          options.body = JSON.stringify(body);
        }

        const response = await fetch(url, options);
        if (!response.ok) throw new Error(response.statusText);

        const json = await response.json();
        setData(json);
      } catch (e) {
        console.error(e.message);
        setError(e);
      } finally {
        setLoading(false);
      }
    };
    fetchData();
  }, [url, method, JSON.stringify(body), JSON.stringify(headers)]);

  return {
    data,
    loading,
    error,
  };
};

function App() {
  const baseUrl = "https://jsonplaceholder.typicode.com/posts";

  const {
    data: getData,
    loading: getLoading,
    error: getError,
  } = useFetch(`${baseUrl}/1`, "GET");

  const {
    data: postData,
    loading: postLoading,
    error: postError,
  } = useFetch(`${baseUrl}`, "POST", {
    userId: 1,
    id: 1,
    title: "hey there !",
    body: "it's POST call from my customHook useFetch()",
  });

  const {
    data: putData,
    loading: putLoading,
    error: putError,
  } = useFetch(`${baseUrl}/1`, "PUT", {
    id: 1,
    title: "hey there !!",
    body: "it's PUT call from my customHook useFetch()",
    userId: 1,
  });

  const {
    data: patchData,
    loading: patchLoading,
    error: patchError,
  } = useFetch(`${baseUrl}/1`, "PUT", {
    title: "hey there !!!",
  });
  const {
    data: deleteData,
    loading: deleteLoading,
    error: deleteError,
  } = useFetch(`${baseUrl}/1`, "DELETE");

  if (getLoading || postLoading || putLoading || patchLoading || deleteLoading)
    return (
      <p>
        {getLoading && "get loading..."}
        {postLoading && "post loading..."}
        {putLoading && "put loading..."}
        {patchLoading && "patch loading..."}
        {deleteLoading && "delete loading..."}
      </p>
    );

  if (getError || postError || putError || patchError || deleteError)
    return (
      <p>
        Error:{" "}
        {
          (getError || postError || putError || patchError || deleteError)
            .message
        }
      </p>
    );

  return (
    <div
      className="App"
      style={{
        maxWidth: "70vw",
        border: "1px solid white",
        padding: "1rem",
        margin: "1rem auto",
      }}
    >
      <h2>useFetch() - custom hook for calling fetch api</h2>

      <h2>GET Response:</h2>
      <p>{JSON.stringify(getData, null, 2)}</p>

      <h2>POST Response:</h2>
      <pre>{JSON.stringify(postData, null, 2)}</pre>

      <h2>PUT Response:</h2>
      <pre>{JSON.stringify(putData ?? "PUT request success", null, 2)}</pre>

      <h2>PATCH Response:</h2>
      <pre>{JSON.stringify(patchData ?? "PATCH request success", null, 2)}</pre>

      <h2>DELETE Response:</h2>
      <pre>
        {JSON.stringify(deleteData ?? "DELETE request success", null, 2)}
      </pre>
    </div>
  );
}

export default App;
