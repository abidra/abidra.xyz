---
title: Next.js Authentication Layout using React High Order Component (HOC)
author: Abid Rakhmansyah
pubDatetime: 2024-10-02T08:02:59.189Z
postSlug: nextjs-authentication-layout-using-react-high-order-component
featured: false
draft: false
tags:
  - react.js
  - next.js
description: Create Authentication Layout using React Hight Order Component (HOC)
---

While working with Next.js, I noticed that authentication is one of the most essential components in any application. With the introduction of the new App Router in Next.js, there have been significant changes in how layouts and routing are handled. These updates differ substantially from the previous versions that used the Pages Router. In this article, I will explain how to create a new authentication layout using the App Router in Next.js.

## Table of contents

## Introduction

Before diving into how to create a new authentication layout, I would first like to explain React's Higher-Order Components (HOCs). HOCs are an advanced technique for reusing component logic. They follow a pattern where a function takes a component as an argument and returns a new component with enhanced functionality. This allows you to reuse logic across multiple components without altering their structure. By utilizing HOCs, you can easily integrate your authentication logic into any layout.

## Prerequisite

Make sure your Next.js application are running on App Router.

## Create a new Authentication Layout

In this step, you will create separate authentication layouts for both authenticated and non-authenticated users. The authenticated user layout will wrap pages that require authentication, commonly referred to as a protected route. Conversely, the non-authenticated user layout will wrap pages that do not require authentication.

### Authenticated Layout:

```typescript
'use client';

import useAuth from '@/hooks/useAuth';
import { useRouter } from 'next/navigation';
import { useEffect, ComponentType } from 'react';

interface AuthProps {
  [key: string]: any;
}

export default function withAuth<T extends AuthProps>(
  Component: ComponentType<T>,
) {
  return function AuthenticatedComponent(props: T) {
    const { isAuthenticated, loading } = useAuth();
    const router = useRouter();

    useEffect(() => {
      if (!loading && !isAuthenticated) {
        router.push('/auth/login');
      }
    }, [isAuthenticated, loading, router]);

    if (loading) return null;

    return isAuthenticated ? <Component {...props} /> : null;
  };
}

```

### Non Authenticated Layout:

```typescript
'use client';

import useAuth from '@/hooks/useAuth';
import { usePathname, useRouter } from 'next/navigation';
import { ComponentType, useEffect } from 'react';

interface NoAuthProps {
  [key: string]: any;
}

export default function withNoAuth<T extends NoAuthProps>(
  Component: ComponentType<T>,
) {
  return function NotAuthenticatedComponent(props: T) {
    const { isAuthenticated, loading } = useAuth();
    const router = useRouter();

    useEffect(() => {
      if (!loading && isAuthenticated) {
        router.push('/dashboard');
      }
      // eslint-disable-next-line react-hooks/exhaustive-deps
    }, [isAuthenticated, loading, pathname, router]);

    if (loading) return null;

    return isAuthenticated ? null : (
      <Component {...props} />
    );
  };
}

```

## How to use it

### Authenticated

To establish a consistent structure across your application's routes, the first step is to create a `layout.tsx` file. This file will act as a wrapper to define the layout used throughout a specific route. In this example, I'll guide you through setting up a layout that requires authentication. This ensures that only authenticated users can access the content within the layout, thereby providing a layer of security for protected routes. The layout file will include logic to verify user authentication status before rendering any components, as demonstrated in the following example:

```typescript
'use client';

import React, { useEffect } from 'react';
import withAuth from '@/hoc/withAuth';

const ProtectedLayout = ({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) => {
  return (
  // Your layout logic
  );
};

export default withAuth(ProtectedLayout);

```

### Non Authenticated

To set up a consistent layout across your application routes, start by creating a layout.tsx file. This file will serve as a wrapper for the route's content, allowing you to define a shared structure or styling. For this example, I will demonstrate how to create a layout that does not require authentication, making it suitable for public-facing pages. This approach ensures that components rendered within this layout will maintain a unified look and feel without any authentication barriers, as illustrated in the following example:

```typescript
'use client';

import React, { useEffect } from 'react';
import withNoAuth from '@/hoc/withNoAuth';

const PublicLayout = ({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) => {
  return (
  // Your layout logic
  );
};

export default withNoAuth(PublicLayout);

```

## Conclusion

By implementing a Higher-Order Component (HOC) for the authentication layout, you can streamline the process of setting up layouts for individual pages, making it significantly faster and more convenient. With this approach, you only need to configure two components based on specific conditions, and the HOC will automatically apply the appropriate layout across multiple pages. This not only simplifies the layout setup but also improves the maintainability of your code by centralizing the layout logic within the HOC. As a result, any changes or updates to the layout can be easily managed in one place, ensuring consistency and reducing the risk of errors.
