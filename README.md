async function iterateWithAsyncAwait(values) {
  for (const value of values) {
    await new Promise((resolve) => setTimeout(resolve, 1000)); 
    console.log(value);
  }
}

const values = [1, 2, 3, 4, 5];
iterateWithAsyncAwait(values);

async function awaitCall() {
  const simulateApiCall = () =>
    new Promise((resolve) => {
      setTimeout(() => resolve({ data: 'API Response Data' }), 2000);
    });

  const response = await simulateApiCall();
  console.log(response.data);
}

awaitCall();

async function awaitCallWithErrorHandling() {
  const simulateApiCall = () =>
    new Promise((resolve, reject) => {
      setTimeout(() => reject(new Error('Failed to fetch data')), 2000);
    });

  try {
    const response = await simulateApiCall();
    console.log(response.data);
  } catch (error) {
    console.log('Error fetching data:', error.message);
  }
}

awaitCallWithErrorHandling();

async function concurrentRequests() {
  const fetchData1 = () =>
    new Promise((resolve) => setTimeout(() => resolve('Data from API 1'), 2000));

  const fetchData2 = () =>
    new Promise((resolve) => setTimeout(() => resolve('Data from API 2'), 3000));

  const [response1, response2] = await Promise.all([fetchData1(), fetchData2()]);
  console.log('Combined Results:', response1, response2);
}

concurrentRequests();

async function parallelCalls(urls) {
  const fetchData = (url) =>
    new Promise((resolve) =>
      setTimeout(() => resolve(`Data from ${url}`), Math.random() * 2000)
    );

  const results = await Promise.all(urls.map((url) => fetchData(url)));
  console.log('Responses:', results);
}

const urls = ['https://api1.com', 'https://api2.com', 'https://api3.com'];
parallelCalls(urls);
