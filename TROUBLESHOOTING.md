# Troubleshooting

## Configuring HTTPS Forwarding Profile

| Error Code | Possible Cause | Solve | 
| --- | --- |  --- | 
| __server error - 405 Method Not Allowed__ | Could be incorrect method usage or missing authentication headers. | Make sure the app can correctly handle the PaloAlto POST request | 
| __server communication error__ | The URL may be incorrect or application may be stopped | Check URL or try setting the app to be 'Always On' (__Azure Portal > web app > configuration > Always on__ ) |
| __server authentication failed__ | The API is attempting to POST to the web app Development site|Check URL is for the public site and not the development site (Development site url contains '.scm' |
| __AxiosError: Request failed with status code 400__ | The Strata Cloud Manager/Logging Service authentication session has timed out | Sign out of Prisma Access portals and sign back in |

