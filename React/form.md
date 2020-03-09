# All about form in react

## Formik

```jsx harmony
import React from "react";
import {Formik, Field, ErrorMessage, Form, useField} from "formik";
import * as Yup from 'yup';


const Login = () => {
  const initialValues = { firstName: '', lastName: '', email: '' };
  const MyTextInput = ({ label, ...props }) => {
    // useField() returns [formik.getFieldProps(), formik.getFieldMeta()]
    // which we can spread on <input> and also replace ErrorMessage entirely.
    const [field, meta] = useField(props);
    console.log(field);
    return (
      <div>
        <label htmlFor={props.id || props.name}>{label}</label>
        <input className="text-input" {...field} {...props} />
        {meta.touched && meta.error ? (
          <div className="error">{meta.error}</div>
        ) : null}
      <div/>
    );
  };
  return (
    <Formik
      initialValues={initialValues}
      validationSchema={Yup.object({
        firstName: Yup.string()
          .max(15, 'Must be 15 characters or less')
          .required('Required'),
        lastName: Yup.string()
          .max(20, 'Must be 20 characters or less')
          .required('Required'),
        email: Yup.string()
          .email('Invalid email address')
          .required('Required'),
      })}
      onSubmit={(values, { setSubmitting }) => {
        setTimeout(() => {
          alert(JSON.stringify(values, null, 2));
          setSubmitting(false);
        }, 400);
      }}
    >
      <Form>
        <MyTextInput label="First Name" name="firstName" type="text" placeholder="me" />
        <label htmlFor="lastName">Last Name</label>
        <Field name="lastName" type="text" />
        <ErrorMessage name="lastName" />
        <label htmlFor="email">Email Address</label>
        <Field name="email" type="email" />
        <ErrorMessage name="email" />
        <button type="submit">Submit</button>
      </Form>
    </Formik>
  );
};

```

## Handle error in form

<div className="content">
      <Formik
        initialValues={{
          user: '',
          password: '',
        }}
        onSubmit={formSubmitHandler}
        validationSchema={loginValidationSchema}
      >
        {({ errors, touched }) => (
          <Form className="forms">
            <FormikField
              error={errors.user && touched.user}
              name="user"
              type="input"
              placeholder="Username"
            />
            <FormikField
              error={errors.password && touched.password}
              name="password"
              type="password"
              placeholder="Password"
            />
            <Button type="submit" variant="contained" color="primary" size="large">
              Login
            </Button>
          </Form>
        )}
      </Formik>
    </div>
```
