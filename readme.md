# bottle-cors-plugin

The most easy way to implement cors on your bottle py web application

## Installing the plugin

    pip install bottle-cors-plugin

after this on your bottle app you need to import cors_plugin and install
for example.

    # -*- coding: utf-8 -*-
    from bottle import app, response, route, run
    from cors import cors_plugin

    @route('/', method='GET')
    def landing():
      response.content_type = 'application/json'
      return {'status': 'Works'}

    #Confugure the server
    app = app()
    app.install(cors_plugin('*'))

    if name == "__main__":
      run(host='localhost', port=7000)

On the cors_plugin function you can send a simple string or array of origins
this variable will set globaly on the plugin so you just set-it one time

    cors_plugin('*')

or

    cors_plugin(['google.com', 'youtube.com'])

## On abort

for normal abort errors you need to import the abort of the cors_plugin like
this

    from bottle_cors_plugin import abort


    @route('/', method='GET')
    def landing():
      response.content_type = 'application/json'
      abort(500, 'Hola')
      return {'status': 'Works'}

It works with all errors, and for custom error handler just import the cors_headers
to apply on the function example like this

    # -*- coding: utf-8 -*-
    from import_env import os
    from bottle import error, response
    from bottle_cors_plugin import cors_headers

    error_log = error

    for status_code in range(200, 600):
    @error(status_code)
    def errorCustom(error_log):
        cors_headers()
        error_log.content_type = 'application/json'
        return error_log.body
