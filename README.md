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
