# Simply Vulnerable Application
## Using React and Express

The purpose of this application is to demonstrate vulnerabilities when using React.  Since React is a front-end framework, most of the vulnerabilities are going to be DOM XSS related.  Some of these examples are created to mimic architectural patterns observed in single-page applications developed using a variety of front-end frameworks.

Most output using React is escaped by default.  It generally requires using the `dangerouslySetInnerHTML` attribute to bypass React's escaping mechanism.  It is also possible to write directly into the DOM via non-React DOM manipulation methods.


## How to Run

### Running the API
The API serves the backend portions of the test application.  To run it, execute the following commands in a terminal:

```
cd api
npm install
npm start
```

The server starts and listens for connections on port 9000.

### Running the React application

The React application demonstrates various vulnerabilities.  To run the React application, execute the following commands in a terminal:

```
cd client
npm install
npm start
```

# Detectable Vulnerabilities

These are spots where vulnerabilities should be detected.


## `client-side-xss/client-side-xss.jsx`

This is a base class for many React components in the project.  This line should be detected as a location where a vulnerability is found:

```
<div dangerouslySetInnerHTML={{ __html: this.props.genericInput }} />
```


## `client-side-xss/embedded.jsx`

The `InnerElement` function is a React component that has a vulnerability in these lines:

```
<div className="result" dangerouslySetInnerHTML={{ __html: script }} />
<div dangerouslySetInnerHTML={{ __html: props.genericInput }} />
```

This may not be considered a vulnerability considering the source


## `client-side-xss/href.jsx`

Places a value in href.  These lines contain vulnerabilities:

```
<a className="result" href={this.state.href}>ClickMe</a>
div dangerouslySetInnerHTML={{ __html: this.props.genericInput }} />
```

## `client-side-xss/logical.jsx`

There are no vulnerabilities in this file.


## `client-side-xss/queryparams.jsx`

These lines contain vulnerabilities:

```
<div className="result" dangerouslySetInnerHTML={{ __html: this.state.submittedFormValue }} />
<div dangerouslySetInnerHTML={{ __html: this.props.genericInput }} />

```

## `client-side-xss/reactdom_escaped.jsx`

There are no vulnerabilities in this file.


## `client-side-xss/reactdom_vulnerable.jsx`

These lines contain vulnerabilities:

```
<div className="result" dangerouslySetInnerHTML={{ __html: this.state.submittedFormValue }} />
<div dangerouslySetInnerHTML={{ __html: this.props.genericInput }} />

```

## `client-side-xss/safe_render_func.jsx`

There are no vulnerabilities in this file.

## `client-side-xss/safe_render_lambda.jsx`

There are no vulnerabilities in this file.

## `client-side-xss/safe.jsx`

There are no vulnerabilities in this file.


## `client-side-xss/vulnerable_render_func.jsx`

These lines contain vulnerabilities:

```
--&gt;<div dangerouslySetInnerHTML={{ __html: props.injectable }} />&lt;--
```

## `client-side-xss/vulnerable_render_lambda.jsx`

These lines contain vulnerabilities:

```
--&gt;<div dangerouslySetInnerHTML={{ __html: props.injectable }} />&lt;--
```

## `client-side-xss/vulnerable.jsx`

These lines contain vulnerabilities:

```
document.getElementById('targetDiv').innerHTML = this.state.formValue;
```

## `server-side-xss/remote_render_funcs.jsx`

In the function `UnsafeRenderFunc` these lines contain vulnerabilities:

```
Unsafe: <div className="result" dangerouslySetInnerHTML={{ __html: props.val }} />
<div dangerouslySetInnerHTML={{__html: props.genericInput}}/>
```

## `server-side-xss/remote_safe.jsx`

There are no vulnerabilities in this file.

## `server-side-xss/remote_unsafe.jsx`

These lines contain vulnerabilities:

```
<div className="result" dangerouslySetInnerHTML={{ __html: this.state.injected }} />
<div dangerouslySetInnerHTML={{__html: this.props.genericInput}} />

```

