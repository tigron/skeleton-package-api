# skeleton-package-api

## Description

This library enables an API for a Skeleton project


## Installation

Installation via composer:

    composer require tigron/skeleton-package-api

## Howto

Create an index module in your application that extends from Skeleton\Package\Api\Web\Module\Index

	<?php
	/**
	 * Module Index
	 *
	 * @author Christophe Gosiau <christophe@tigron.be>
	 * @author Gerry Demaret <gerry@tigron.be>
	 * @author David Vandemaele <david@tigron.be>
	 */

	class Web_Module_Index extends \Skeleton\Package\Api\Web\Module\Index {
	}

This module will creates a user interface for the API. The user interface is
based on docblocks in the call-modules


Create a call-module

	<?php
	/**
	 * Module Index
	 *
	 * @author Christophe Gosiau <christophe@tigron.be>
	 * @author Gerry Demaret <gerry@tigron.be>
	 * @author David Vandemaele <david@tigron.be>
	 */

	class Web_Module_User extends \Skeleton\Package\Api\Web\Module\Call {

		/**
		 * Get by id
		 *
		 * Get a user by his ID
		 *
		 * @access public
		 * @param int $id
		 * @return array $user
		 */
		public function call_getById() {
			$user = User::get_by_id($_REQUEST['id']);
			return $user->get_info();
		}
	}

Make sure every call method is prepended with 'call_'.
Also make sure to the docblocks contains the correct variables. These will be
available as $_REQUEST parameters

## Security

Each API request is checked for correct credentials. The API keys can be configured via:

    \Skeleton\Package\Api\Config::$api_keys = [ 'KEY1', 'KEY2' ];

Each API call now needs to contain a valid API KEY in its GET-parameters

    http://api.myapplication.tld/user?call=getById&id=1&api_key=KEY1

To disable authentication, set the Config-value to false

    \Skeleton\Package\Api\Config::$api_keys = false;

For more control, each call will execute a 'secure-method' before proceeding. If
your application needs more fine-grained user permissions, you can implement
them here.


		/**
		 * Secure
		 *
		 * @access public
		 * @return bool $secured
		 */
		public function secure() {
		    $api_key = $_REQUEST['api_key'];
		    // Only keys that start with letter A are allowed
		    if ($api_key[0] == 'A') {
		    	return true;
		    }
		    return false;
		}
