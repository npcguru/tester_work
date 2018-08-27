/**
 * ダミーのsvgを作成する
 * @return {Response}
 */
function createDummySvgResponse() {
    let headers = new Headers();
      headers.append('Content-Type', 'image/svg+xml');
      let body = `<svg height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><circle cx="12" cy="12" r="10" stroke="#000" fill="none" /></svg>`
      return new Response(body, {headers})
  }
  
  // htmlからリクエストが飛ぶと呼ばれる
  // 通常はここでweb上のファイルを取りに行くが
  // それをフックしてダミーのsvgファイルを返す
  self.addEventListener('fetch', function(event) {
    if (event.request.url.indexOf('hoge.svg') != -1) {
      const response = createDummySvgResponse()
      event.respondWith(response);
      return
    }
    
    // 上記if文に入らなかったものは、普通にwebから取得される
  });