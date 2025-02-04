The CORS plugin lets you add cross-origin resource sharing (CORS) to a service or a route.

## CORS limitations

If the client is a browser, there is a known issue with this plugin caused by a
limitation of the [CORS specification](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) that prevents specifying a custom
`Host` header in a preflight `OPTIONS` request.

Because of this limitation, this plugin only works for routes that have been
configured with a `paths` setting. The CORS plugin does not work for routes that
are being resolved using a custom DNS (the `hosts` property).

To learn how to configure `paths` for a route, read the [Proxy Reference](/gateway/latest/reference/proxy).
