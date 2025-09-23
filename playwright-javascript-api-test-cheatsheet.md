import { test, expect, request } from '@playwright/test';

test('API test example', async ({ request }) => {

  // 1️⃣ GET request
  const response = await request.get('https://jsonplaceholder.typicode.com/posts/1');
  expect(response.status()).toBe(200);
  const body = await response.json();

  // 2️⃣ POST request
  const postResp = await request.post('https://api.example.com/users', {
    data: { name: 'Kaio', email: 'kaio@example.com' }
  });
  const postBody = await postResp.json();
  expect(postBody.id).toBeDefined();

  // 3️⃣ PUT / PATCH request
  const putResp = await request.put('https://api.example.com/users/1', {
    data: { name: 'Kaio Updated' }
  });
  expect(putResp.status()).toBe(200);

  // 4️⃣ DELETE request
  const delResp = await request.delete('https://api.example.com/users/1');
  expect(delResp.status()).toBe(204);

  // 5️⃣ Headers
  const hdrResp = await request.get('https://api.example.com/users', {
    headers: { 'Authorization': 'Bearer my-token', 'Accept': 'application/json' }
  });

  // 6️⃣ Query params
  const paramResp = await request.get('https://api.example.com/users', {
    params: { page: 1, limit: 10 }
  });

  // 7️⃣ Assertions
  expect(response.status()).toBe(200);
  expect(await response.text()).toContain('Kaio');
  expect(await response.json()).toHaveProperty('id');

  // 8️⃣ Chaining requests
  const createResp = await request.post('/users', { data: { name: 'Kaio' } });
  const user = await createResp.json();
  await request.put(`/users/${user.id}`, { data: { name: 'Kaio Updated' } });
  const getResp = await request.get(`/users/${user.id}`);
  expect(await getResp.json()).toMatchObject({ name: 'Kaio Updated' });

  // 9️⃣ APIRequestContext for custom configs
  const apiContext = await request.newContext({
    baseURL: 'https://api.example.com',
    extraHTTPHeaders: { 'Authorization': 'Bearer my-token' }
  });
  const ctxResp = await apiContext.get('/users');

  // 🔟 Uploading files
  const uploadResp = await request.post('https://api.example.com/upload', {
    multipart: { file: { name: 'test.txt', mimeType: 'text/plain', buffer: Buffer.from('Hello World') } }
  });
  expect(uploadResp.status()).toBe(201);

  // 1️⃣1️⃣ Downloading files
  const downloadResp = await request.get('https://api.example.com/report.pdf');
  const buffer = await downloadResp.body();
  require('fs').writeFileSync('report.pdf', buffer);

});
