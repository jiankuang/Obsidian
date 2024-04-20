### SPA 
A Single-Page Application (SPA) works by rendering and data fetching taking place in the browser itself. This results in the First Contentful Paint (FCP) taking longer, affecting the user experience. 
### SSR 
In contrast, SSR (Server Side Render) mitigates these issues by rendering the initial page in the server itself, reducing the time taken for FCP and vastly improving the user experience. However, the page will not become interactive immediately, and the browser needs to wait till it completes downloading the JavaScript bundle to add interactivity. 
### RSC
RSC (React Server Component) is a new way of doing server-side rendering by allowing developers to write components that run on the server and stream their output to the client. 
In RSC, there are two types of components: server components, which can be rendered on the server, and client components, which are rendered on the browser. Server component can be defined as any component that doesn't involve user interactivity like a mouse click or keyboard input or use React hooks like the useState hook and the useEffect hook. 
### RSC vs. SSR
In contrast, SSR performs server-side rendering only during the initial page load. This means that other than the initial components, all other components are rendered in the browser when SSR is used. So, the browser has to download the JavaScript for the whole app just like in a Single-Page Application (SPA). This makes SRC more efficient than SSR in terms of performance and user experience. 